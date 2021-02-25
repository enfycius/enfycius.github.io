---
title: "OpenCV 과제: 영상 색상 채우기 #2"

classes: wide

categories:
  - OpenCV
  - Algorithms
tags:
  - OpenCV
  - Algorithms
  - Programming
  - Coding

toc: true
---

# 질문

## 내용

다음 영상 이름은 "hwfig5-1.jpg"이다. 이 영상에 대해 다음을 프로그래밍하시오.

![hwfig5-1.jpg](/assets/images/opencv/assignment/opencv-assign-1.jpg)

1. 위 영상을 Mat img1 = imread() 함수를 이용하여 grayscale 영상으로 읽어 오시오.

2. 또 다른 영상을 저장하기 위해 Mat img2;로 하고, 이것은 칼라(3채널)로 저장하기 위해 선언하시오.

3. 위 영상에 대해 히스토그램을 구하시오.

4. 히스토그램에서 최대 peak가 되는 값 4개를 구하시오. (육안으로...)

5. 각 4개 peak점의 가운데 값을 문턱치로 사용하여 가장 어두운 직사각형은 파랑색, 원은 녹색, 삼각형은 빨강색, 배경은 노랑색으로 하여 img2를 만들어 display하시오.

# 답변

## 내용

그럼 1편에 이어서 위 문제를 풀이해보겠다.

이제 4번을 풀이할 차례이다.

먼저 1편에서 완성시킨 아래의 히스토그램을 다시 살펴보면, 히스토그램이 굉장히 매끄럽지 못한 것을 확인해볼 수 있다.

![Before_Histogram](/assets/images/opencv/assignment/opencv-assign-2.png)

그래서 필자는 히스토그램을 그리기 전(draw_Histogram 함수를 호출하기 전)에 Gaussian Filter(Blur)를 적용하여 Smooth한 히스토그램을 만들어보려 한다.

먼저 1편에서 작성한 전체 코드를 가져오자.

```cpp
#include <opencv2/opencv.hpp>

using namespace cv;

Mat draw_Histogram(Mat& hist) {
    int hist_w = 2048;
    int hist_h = 500;
    int hist_size = 350;
    int bin_w = cvRound((double)hist_w/hist_size);

    Mat histImage(hist_h, hist_w, CV_8UC3, Scalar(0, 0, 0));

    normalize(hist, hist, 0, histImage.rows, NORM_MINMAX, -1, Mat());

    for(int i=1; i<hist_size; i++) {
        Point pts[] = {Point(bin_w * (i-1), hist_h), Point(bin_w * i, hist_h), Point(bin_w * i, hist_h - cvRound(hist.at<float>(i))), Point(bin_w*(i-1), hist_h-cvRound(hist.at<float>(i-1))), Point(bin_w*(i-1), hist_h)};

        fillConvexPoly(histImage, pts, 5, Scalar(255, 255, 255));
    }

    imshow("Histogram", histImage);

    return histImage;
}

int main(void) {
    int histSize = 350;

    float range[] = {0, 256};
    const float* histRange = {range};

    bool uniform = true, accumulate = false;
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);

    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    histImg = draw_Histogram(b_hist);
    
    waitKey(0);

    return 0;
}
```

필자가 위에서 언급했듯이 히스토그램을 그리기 전에 즉, draw_Histogram 함수를 호출하기 전에 b_hist에 대하여 Gaussian Filter를 적용해야 하는데, 이를 위해 공식적으로 제공하는 GaussianBlur 함수를 이용하자.

GaussianBlur 함수는 다음과 같다.

```cpp
void GaussianBlur(InputArray src, OutputArray dst, Size ksize, double sigmaX, double sigmaY=0, int borderType=BORDER_DEFAULT)
```

각 매개변수에 대한 설명은 아래의 사이트를 참고해보자.

[Reference](http://docs.opencv.org/2.4/modules/imgproc/doc/filtering.html?highlight=gaussianblur#gaussianblur)

필자는 9X9의 가우시안 필터를 적용했다.

아래의 코드를 통해 이를 확인해보자.

```cpp
#include <opencv2/opencv.hpp>

using namespace cv;

Mat draw_Histogram(Mat& hist) {
    int hist_w = 2048;
    int hist_h = 500;
    int hist_size = 350;
    int bin_w = cvRound((double)hist_w/hist_size);

    Mat histImage(hist_h, hist_w, CV_8UC3, Scalar(0, 0, 0));

    normalize(hist, hist, 0, histImage.rows, NORM_MINMAX, -1, Mat());

    for(int i=1; i<hist_size; i++) {
        Point pts[] = {Point(bin_w * (i-1), hist_h), Point(bin_w * i, hist_h), Point(bin_w * i, hist_h - cvRound(hist.at<float>(i))), Point(bin_w*(i-1), hist_h-cvRound(hist.at<float>(i-1))), Point(bin_w*(i-1), hist_h)};

        fillConvexPoly(histImage, pts, 5, Scalar(255, 255, 255));
    }

    imshow("Histogram", histImage);

    return histImage;
}

int main(void) {
    int histSize = 350;

    float range[] = {0, 256};
    const float* histRange = {range};

    bool uniform = true, accumulate = false;
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);

    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    GaussianBlur(b_hist, b_hist, Size(9, 9), 0);        // 9x9 가우시안 필터 적용

    histImg = draw_Histogram(b_hist);
    
    waitKey(0);

    return 0;
}
```

그 결과는 다음과 같다.

![After_Histogram](/assets/images/opencv/assignment/opencv-assign-3.png)

전보다 매끄러운 히스토그램이 도출된 것을 확인해볼 수 있다.

이제 도출된 히스토그램 위의 Peaks들에 Line을 그려줘야 하는데, 이를 위해 먼저 Peaks 값을 찾는 함수를 작성하고, 찾은 값들에 대해서 실제로 Line을 그려주는 함수를 작성해보자.

필자는 Peaks 값을 찾는 함수의 이름을 find_Peaks로 지었으며, Mat Reference Type의 src라는 이름의 매개변수를 선언했다.

또한, 찾은 Peaks들의 값(int형)을 저장한 vector 자료형을 반환할 것이므로 반환형은 std::vector\<int\>로 했다.

즉, 이를 코드로 보이면 다음과 같다.

```cpp
std::vector<int> find_Peaks(Mat& src) {

}
```

이제 Peaks들의 값을 찾아야 하는데, 사실 극댓값을 찾는 알고리즘을 작성하여 이를 해결해도 되지만, 불연속점의 존재 가능성(실제로 불연속적이어도 극댓값은 존재한다.)과 같이 다양한 상황에 적용되는 일반적인 알고리즘을 개발하기가 상당히 까다롭기 때문에 필자는 위 이미지의 히스토그램에 적용되는 더 쉬운 방법을 이용해 이를 해결해봤다.

그것은 바로 OpenCV에서 공식적으로 제공하고 있는 minMaxLoc Function을 이용하는 것이다.

minMaxLoc Function은 다음과 같다.

```cpp
void cv::minMaxLoc(InputArray src,
                   double* minVal,
                   double* maxVal = 0,
                   Point* minLoc = 0,
                   Point* maxLoc = 0,
                   InputArray mask = noArray()
)
```

위 Function에 대한 더 자세한 사항은 아래 링크를 참고해보자.

[Reference](https://docs.opencv.org/3.4/d2/de8/group__core__array.html#gab473bf2eb6d14ff97e89b355dac20707)

minMaxLoc Function은 히스토그램의 최댓값을 찾아주는 Function인데, 그러면 여기서 드는 생각이

> 최댓값만 찾을 수 있다면, 다른 히스토그램의 최댓값은 찾을 수 없는 것 아닌가요?

이다.

그래서 필자는 다음의 Trick을 이용했다.

먼저 원본 히스토그램 이미지의 유지를 위해(위에 Line을 그려야 하므로) 히스토그램 이미지의 복제본을 하나 생성한다.

복제된 이미지에 대해서 minMaxLoc Function을 호출한다.

그러면 당연히 4개의 히스토그램 중 가장 높은 Peak 값을 가지는 히스토그램(위의 이미지에서는 가장 오른쪽 히스토그램)의 Peak값이 도출될 것이다.

그 값을 별도로 저장한 후, 0(최솟값)으로 변경해버리고 히스토그램의 주변 반경에 있는 값들 역시 모두 0(최솟값)으로 변경해버리자. 

만약 주변 반경에 있는 값들을 처리하지 않았을 경우에 다시 한번 minMaxLoc Function을 호출하게 되면, 두 번째로 높은 Peak 값을 가지는, 왼쪽에서 두 번째에 위치한 히스토그램의 Peak 값이 도출되는 것이 아니라 가장 오른쪽 히스토그램의 두 번째 최댓값이 도출되게 된다.

이러한 아이디어를 바탕으로 필자는 다음의 코드를 작성할 수 있었다.

(편의를 위해 std 이름 공간을 사용했다고 가정했다.)

```cpp
vector<int> find_Peaks(Mat& src) {
    vector<int> peaks;      // peaks들의 값을 저장할 변수
    Mat dup_src;            // 매개변수 src를 복제하여 저장할 변수
    
    Point p;        // 히스토그램의 최대 Peak 값을 저장하는 변수
    
    dup_src = src.clone();      // 매개변수 src를 복제하여 dup_src에 담는다.
    
    for(int i=0; i<4; i++) {    // 위 이미지에서 보여지는 히스토그램이 4개 있으므로, 4회 반복.
        minMaxLoc(dup_src, 0, 0, 0, &p);       // 우리는 히스토그램의 Peak 값만 필요하므로 최댓값과 최솟값을 저장할 변수는 필요치 않음.
        peaks.push_back(p.y);       // 위치 값 중 y값만을 peaks에 담자.
        dup_src.at<float>(p.y) = 0;        // 최솟값인 0을 넣자.

        for(int j=0; j<10; j++) {           // p.y의 주변 반경 10만큼을 최솟값 0으로 채운다.
            dup_src.at<float>(p.y-(j+1)) = 0;   
            dup_src.at<float>(p.y+(j+1)) = 0;
        }
    }
    
    return peaks;       // peaks 값들 반환
}
```

글이 길어질 듯하여 각 코드에 대한 설명을 주석에 달아놓았으니 이를 참고해보자.

(제 코드에 궁금한 점이 있으신 분들께서는 댓글 남겨주세요.)

p.y의 주변 반경 10만큼을 0으로 채우면, 히스토그램이 다음의 과정을 거치는 것을 이미지를 통해 확인해볼 수 있다.

![Histogram](/assets/images/opencv/assignment/opencv-assign-4.png)

![Histogram](/assets/images/opencv/assignment/opencv-assign-5.png)

![Histogram](/assets/images/opencv/assignment/opencv-assign-6.png)

여기까지 완료했다면, 이제 실제로 도출된 Peak의 위치 값을 기반으로 Line을 그려야한다.

필자는 Line을 그려주는 함수의 이름을 draw_Line으로 지었으며, Mat Reference Type의 src와 hist라는 이름의 매개변수를 두 개 선언했다.

또한, peaks 값들로부터 마지막 문항을 해결해야하므로 반환형은 std::vector\<int\>로 선언했다.

즉, 

```cpp
std::vector<int> draw_Line(Mat& src, Mat& hist) {

}
```

Line을 그리는 방법은 OpenCV에서 line Function을 제공하고 있으니, 이를 활용하자.

line Function은 다음과 같다.

```cpp
void cv::line(InputOutputArray img,
              Point pt1,
              Point pt2,
              const Scalar& color,
              int thickness = 1,
              int lineType = LINE_8,
              int shift = 0
)
```

위 함수에 대한 더 자세한 사항은 아래 Reference를 참조하자.

[Reference](https://docs.opencv.org/master/d6/d6e/group__imgproc__draw.html#ga7078a9fae8c7e7d13d24dac2520ae4a2)

먼저 draw_Line Function 내에서 std::vector\<int\>형의 변수를 하나 선언하고, find_Peaks Function을 호출하여 그 반환값을 선언한 변수에 저장하자.

find_Peaks Function을 호출할 때 인자로서 src 매개변수의 값을 보내자.

```cpp
std::vector<int> draw_Line(Mat& src, Mat& hist) {
    std::vector<int> peaks = find_Peaks(src);
}
```

받은 peaks 정보에 대해서 line Function을 이용해 히스토그램 위에 빨간색(Scalar(0, 0, 255)) Line을 그린 후, imshow 함수를 이용해 각 히스토그램의 Peaks들에 Line이 그려진 이미지가 화면에 나오도록 한다.

(편의를 위해 std 이름 공간을 사용했다고 가정했다.)

```cpp
vector<int> draw_Line(Mat& src, Mat& hist) {
    vector<int> peaks = find_Peaks(src);
    int bin_w = cvRound( (double) hist.cols / 350);

    for(size_t i = 0; i < peaks.size(); i++)
        line(hist, Point(bin_w * peaks[i], hist.rows), Point(bin_w * peaks[i], 0), Scalar(0, 0, 255));

    imshow("Peaks", hist);
    return peaks;
}
```

이제 실제 확인을 위해서 main 함수로 돌아가 위에서 작성한 draw_Line Function을 호출하자.

```cpp
int main(void) {
    int histSize = 350;

    float range[] = {0, 256};
    const float* histRange = {range};

    bool uniform = true, accumulate = false;
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);

    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    GaussianBlur(b_hist, b_hist, Size(9, 9), 0);        // 9x9 가우시안 필터 적용

    histImg = draw_Histogram(b_hist);
    
    draw_Line(b_hist, histImg);         // draw_Line Function 호출
    
    waitKey(0);

    return 0;
}
```

이제 프로그램을 실행해보면 다음과 같이 각 히스토그램의 Peaks들에 빨간색 Line이 그려지는 것을 확인해볼 수 있다.

![Result](/assets/images/opencv/assignment/opencv-assign-7.png)

전체 코드를 보이면서 이번 포스팅은 일단 여기서 끝맺고, 다음 포스팅에 이어서 마지막 문항을 풀이하도록 하겠다.

### 전체 코드

```cpp
#include <opencv2/opencv.hpp>

using namespace cv;
using namespace std;

vector<int> find_Peaks(Mat& src) {
    vector<int> peaks;      // peaks들의 값을 저장할 변수
    Mat dup_src;            // 매개변수 src를 복제하여 저장할 변수
    
    Point p;        // 최댓값의 위치를 저장하는 변수
    
    dup_src = src.clone();      // 매개변수 src를 복제하여 dup_src에 담는다.
    
    for(int i=0; i<4; i++) {    // 위 이미지에서 보여지는 히스토그램이 4개 있으므로, 4회 반복.
        minMaxLoc(dup_src, 0, 0, 0, &p);       // 우리는 히스토그램의 Peak 값만 필요하므로 최댓값과 최솟값을 저장할 변수는 필요치 않음.
        peaks.push_back(p.y);       // 위치 값 중 y값만을 peaks에 담자.
        dup_src.at<float>(p.y) = 0;        // 최솟값인 0을 넣자.

        for(int j=0; j<10; j++) {           // p.y의 주변 반경 10만큼을 최솟값 0으로 채운다.
            dup_src.at<float>(p.y-(j+1)) = 0;   
            dup_src.at<float>(p.y+(j+1)) = 0;
        }
    }
    
    return peaks;       // peaks 값들 반환
}

vector<int> draw_Line(Mat& src, Mat& hist) {
    vector<int> peaks = find_Peaks(src);
    int bin_w = cvRound( (double) hist.cols / 350);

    for(size_t i = 0; i < peaks.size(); i++)
        line(hist, Point(bin_w * peaks[i], hist.rows), Point(bin_w * peaks[i], 0), Scalar(0, 0, 255));

    imshow("Peaks", hist);
    return peaks;
}

Mat draw_Histogram(Mat& hist) {
    int hist_w = 2048;
    int hist_h = 500;
    int hist_size = 350;
    int bin_w = cvRound((double)hist_w/hist_size);

    Mat histImage(hist_h, hist_w, CV_8UC3, Scalar(0, 0, 0));

    normalize(hist, hist, 0, histImage.rows, NORM_MINMAX, -1, Mat());

    for(int i=1; i<hist_size; i++) {
        Point pts[] = {Point(bin_w * (i-1), hist_h), Point(bin_w * i, hist_h), Point(bin_w * i, hist_h - cvRound(hist.at<float>(i))), Point(bin_w*(i-1), hist_h-cvRound(hist.at<float>(i-1))), Point(bin_w*(i-1), hist_h)};

        fillConvexPoly(histImage, pts, 5, Scalar(255, 255, 255));
    }

    imshow("Histogram", histImage);

    return histImage;
}

int main(void) {
    int histSize = 350;

    float range[] = {0, 256};
    const float* histRange = {range};

    bool uniform = true, accumulate = false;
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);

    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    GaussianBlur(b_hist, b_hist, Size(9, 9), 0);        // 9x9 가우시안 필터 적용

    histImg = draw_Histogram(b_hist);
    
    draw_Line(b_hist, histImg);
    
    waitKey(0);

    return 0;
}
```