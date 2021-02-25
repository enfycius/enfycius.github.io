---
title: "OpenCV 과제: 영상 색상 채우기 #3 - 최종"

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

그럼 2편에 이어서 위 문제를 풀이해보겠다.

이제 5번을 풀이할 차례이다.

2편에서 작성한 전체 코드를 가져오자.

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

draw_Line Function은 우리가 2편에서 작성했었던 것처럼 std::vector\<int\>형의 peaks 변수를 반환했기 때문에 main 함수에서 이를 받아야 median 값을 도출할 수 있다.

그러므로 std::vector\<int\>형의 peaks를 main 함수 내에 하나 선언한 후, peaks를 받자.

즉,

```cpp
int main(void) {
    int histSize = 350;

    float range[] = {0, 256};
    const float* histRange = {range};

    bool uniform = true, accumulate = false;

    vector<int> peaks;          // draw_Line Function 반환 값을 저장할 변수 선언
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);

    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    GaussianBlur(b_hist, b_hist, Size(9, 9), 0);        // 9x9 가우시안 필터 적용

    histImg = draw_Histogram(b_hist);
    
    peaks = draw_Line(b_hist, histImg);         // 반환 값을 담자.
    
    waitKey(0);

    return 0;
}
```

peaks 내에는 히스토그램의 각 Peaks들의 값이 저장되어 있으므로, 문제의 5번 항목에서 요구하는 것처럼 4개의 Peaks들의 가운데 값, 즉 median 값을 산출하여 이를 문턱치로 사용하자.

우리는 이미 find_Peaks 함수에서 peaks vector에 값을 넣을 때, 가장 큰 히스토그램의 Peaks 값들부터 순차적으로 넣어줬기 때문에(minMaxLoc Function 덕분이다.) 실제로 peaks vector 내부의 값들은 정렬이 완료된 상태이다.

또한, 총 4개의 Peaks들이 들어가 있으므로, 즉 이는 홀수가 아닌 짝수이므로 가운데를 중심으로 바로 왼쪽에 위치한 원소의 값과 바로 오른쪽에 위치한 원소의 값을 더한 후 2로 나누어주면 중앙값(median)이 도출된다.

이를 코드로 보이면 다음과 같다.

```cpp
int main(void) {
    int histSize = 350;

    float range[] = {0, 256};
    const float* histRange = {range};

    bool uniform = true, accumulate = false;

    vector<int> peaks;          // draw_Line Function 반환 값을 저장할 변수 선언
    double median;              // 중앙값을 저장할 변수 선언
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);

    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    GaussianBlur(b_hist, b_hist, Size(9, 9), 0);        // 9x9 가우시안 필터 적용

    histImg = draw_Histogram(b_hist);
    
    peaks = draw_Line(b_hist, histImg);         // 반환 값을 담자.

    median = (peaks.at((peaks.size()/2)-1) + peaks.at((peaks.size()/2)+1))/2;
    
    waitKey(0);

    return 0;
}
```

위 코드 중 다음의 코드를 보자.

```cpp
median = (peaks.at((peaks.size()/2)-1) + peaks.at((peaks.size()/2)+1))/2;
```

median 값을 도출할 때 필자가 위에서 언급했듯이, peaks 내부에는 총 4개의 Element들이 들어있기 때문에, peaks.size() 즉 peaks의 크기 4를 2로 나눈 후 -1을 하게 되면, 가운데를 중심으로 바로 왼쪽에 위치한 원소의 인덱스 값이 도출된다.

마찬가지 방식으로 가운데를 중심으로 바로 오른쪽에 위치한 원소의 인덱스 값도 peaks.size() 즉 peaks의 크기 4를 2로 나눈 후 +1을 하게 되면 도출된다.

각 인덱스 값에 대응되는 원소의 값들을 불러들여서 서로 더한 후 2로 나누어주면 median 값은 도출된다.

여기까지 완료했다면, 이제 문턱치를 구해보자.

문턱치 값을 구하기 위해서 OpenCV에서는 threshold Function을 제공해주므로, 이를 이용하면 되겠다.

threshold Function은 다음과 같다.

```cpp
double cv::threshold(InputArray src,
                     OutputArray dst,
                     double thresh,
                     double maxval,
                     int type
)
```

위 함수에 대한 더 자세한 설명은 아래의 Reference를 참조하자.

[Reference](https://docs.opencv.org/master/d7/d1b/group__imgproc__misc.html#gae8a4a146d1ca78c626a53577199e9c57)

필자는 흑 또는 백으로만 결과 이미지가 나오게끔 하고 싶기 때문에 type 인자로서 cv::ThresholdTypes인 Threshold Binary를 보내주었다.

또한, 백이 나오려면 maxval의 값은 255가 되어야 하므로, 255를 인자로 보내주었다.

즉 이를 코드로 보이면,

```cpp
int main(void) {
    int histSize = 350;

    float range[] = {0, 256};
    const float* histRange = {range};

    bool uniform = true, accumulate = false;

    vector<int> peaks;          // draw_Line Function 반환 값을 저장할 변수 선언
    double median;              // 중앙값을 저장할 변수 선언
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);

    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성
    Mat dst;        // threshold 처리 후 결과 이미지를 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    GaussianBlur(b_hist, b_hist, Size(9, 9), 0);        // 9x9 가우시안 필터 적용

    histImg = draw_Histogram(b_hist);
    
    peaks = draw_Line(b_hist, histImg);         // 반환 값을 담자.

    median = (peaks.at(peaks.size()/2-1) + peaks.at(peaks.size()/2))/2;

    threshold(img1, dst, median, 255, THRESH_BINARY);       // threshold Function 호출
    
    waitKey(0);

    return 0;
}
```

이렇게 한 후 threshold Function 처리 후의 결과 이미지를 확인해보자.

우리가 위에서 dst Mat 객체를 결과 이미지로 설정했기 때문에 imshow 함수를 이용해서 단순히 dst 이미지를 띄워주기만 하면 된다.

```cpp
int main(void) {
    int histSize = 350;

    float range[] = {0, 256};
    const float* histRange = {range};

    bool uniform = true, accumulate = false;

    vector<int> peaks;          // draw_Line Function 반환 값을 저장할 변수 선언
    double median;              // 중앙값을 저장할 변수 선언
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);

    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성
    Mat dst;        // threshold 처리 후 결과 이미지를 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    GaussianBlur(b_hist, b_hist, Size(9, 9), 0);        // 9x9 가우시안 필터 적용

    histImg = draw_Histogram(b_hist);
    
    peaks = draw_Line(b_hist, histImg);         // 반환 값을 담자.

    median = (peaks.at(peaks.size()/2-1) + peaks.at(peaks.size()/2))/2;

    threshold(img1, dst, median, 255, THRESH_BINARY);

    imshow("Result", dst);
    
    waitKey(0);

    return 0;
}
```

위 코드의 실행 결과가 아래와 같다면 성공이다.

![Result](/assets/images/opencv/assignment/opencv-assign-8.png)

이제 정말 마지막이다.

> 가장 어두운 직사각형은 파랑색, 원은 녹색, 삼각형은 빨강색, 배경은 노랑색으로 하여 img2를 만들어 display하시오.

필자는 위의 threshold Function 처리 결과 도출된 이미지에서 다음과 같은 하나의 패턴을 발견할 수 있었다.

> 흰색, 검은색, 흰색, 검은색, 흰색, 검은색, 흰색의 순서이다.

그래서 필자는 dst 이미지에 대해서 왼쪽에서부터 오른쪽으로 순차적으로 Elements들에 접근하여 만약에 지금 현재 Element의 값이 0이면, 즉 검은색이면 count의 값이 0일 때는 파랑색을, 1일 때는 초록색을, 2일 때는 빨간색을 칠하게끔 작성하였으며, 또 그 다음 Element의 값이 255이면, 즉 흰색이면 count가 2인지 검사하여 만약 그렇다면 다시 0으로, 그렇지 않다면 +1 시키는 방식으로 진행했다.

만약 count의 값이 2일 때 다시 0으로 만들어주는 조건식을 작성하지 않았다면 다음과 같을 것이다.

> 직사각형에서 흰색 배경을 만났을 때 기존 0에서 1로 count의 값이 증가하고, 마찬가지로 원에서 흰색 배경을 만났을 경우에도 기존 count 값인 1에서 2로 증가를 하게 되며, 마지막으로 삼각형에서 흰색 배경을 만났을 때는 count 값이 기존 2에서 3으로 증가한다.

> 문제점을 찾았는가?

필자는 count의 값이 0일 때와 1일 때 그리고 2일 때에 대해서만 그에 맞는 색깔을 칠해주는 조건을 걸었기 때문에 3에 대응되는 조건은 없어서 색깔이 칠해지지 않는 문제가 발생한다.

(더군다나 count의 값은 계속 증가하게 된다.)

그리하여 필자는 count의 값이 2일 때 다시 0으로 만들어주는 조건을 걸어두었다.

이를 코드로 보이면 다음과 같다.

```cpp
int count = 0;                      // count의 값은 0으로 초기화한다.

uchar *data_input = dst.data;       // dst 이미지의 Element에 접근하기 위한 data_input 포인터 변수, 실제 조건의 대상은 dst 이미지이다.

for (int y = 0; y < img2.rows; y++) {
    for (int x = 0; x < img2.cols-1; x++) {
        uchar *data_output = img2.data;     // img2 이미지 위에 색깔을 그리기 위해 Element에 접근하는 data_output 포인터 변수

        if(data_input[y*img2.cols+x] == 0) {        // 현재 Element의 값이 0이면, 즉 검은색이면
            if(count == 0){                         // 그때의 count 값이 0이면, 파랑색
            data_output[y * img2.cols*3 + x*3] = 255;           // B
            data_output[y * img2.cols*3 + x*3 + 1] = 144;       // G
            data_output[y * img2.cols*3 + x*3 + 2] = 30;        // R
            } else if(count == 1) {                 // 그때의 count 값이 1이면, 초록색
                data_output[y * img2.cols*3 + x*3] = 0;         // B
                data_output[y * img2.cols*3 + x*3 + 1] = 128;   // G
                data_output[y * img2.cols*3 + x*3 + 2] = 0;     // R
            }else if(count == 2) {                  // 그때의 count 값이 2이면, 빨강색
                data_output[y * img2.cols*3 + x*3] = 0;         // B
                data_output[y * img2.cols*3 + x*3 + 1] = 0;     // G
                data_output[y * img2.cols*3 + x*3 + 2] = 255;   // R
            }

            if(data_input[y*img2.cols+x+1] == 255) {            // 다음 Element의 값이 255이면, 즉 흰색이면
                if(count == 2)          // 그때의 count 값이 2라면
                    count = 0;          // 0으로 변경
                else                    // 2가 아니라면
                    count++;            // count 값을 1만큼 증가
            }
        }else if(data_input[y*img2.cols+x] == 255) {            // 현재 Element의 값이 255이면, 즉 흰색이면 노랑색
            data_output[y * img2.cols*3 + x*3] = 0;             // B
            data_output[y * img2.cols*3 + x*3 + 1] = 255;       // G
            data_output[y * img2.cols*3 + x*3 + 2] = 255;       // R
        }
    }
}
```

위 코드로부터 알 수 있는 사실은 

> OpenCV에서 Color Image Matrix는 우리가 기존에 알고 있던 R, G, B 순서가 아닌 B, G, R 순서이다.

라는 점과 img2의 경우에는 dst와는 달리 3 channel Matrix라서(img2를 불러들일 때 IMREAD_COLOR로 불러들인 것을 기억하고 있는가?) +0, +1, +2로 각각 B, G, R에 접근할 수 있다는 점이다.

이제 필자가 생각하여 작성한 코드가 문제의 5번 항목에서 요구한 바를 충족시켜주는지를 확인해보자.

img2에 대해서 색깔을 칠해주었으므로 imshow 함수의 인자로 img2를 보내주자.

```cpp
int main(void) {
    int histSize = 350;

    float range[] = {0, 256};
    const float* histRange = {range};

    bool uniform = true, accumulate = false;

    vector<int> peaks;          // draw_Line Function 반환 값을 저장할 변수 선언
    vector<int>::iterator iter;
    
    double median;              // 중앙값을 저장할 변수 선언
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);
    
    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성
    Mat dst;        // threshold 처리 후 결과 이미지를 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    GaussianBlur(b_hist, b_hist, Size(9, 9), 0);        // 9x9 가우시안 필터 적용

    histImg = draw_Histogram(b_hist);
    
    peaks = draw_Line(b_hist, histImg);         // 반환 값을 담자.
    
    for(iter = peaks.begin(); iter != peaks.end(); iter++)
        cout<<*iter<<endl;

    median = (peaks.at((peaks.size()/2)-1) + peaks.at((peaks.size()/2)+1))/2;

    threshold(img1, dst, median, 255, THRESH_BINARY);
    
    uchar *data_input = dst.data;

    int count = 0;

    for (int y = 0; y < img2.rows; y++) {
        for (int x = 0; x < img2.cols-1; x++) {
            uchar *data_output = img2.data;     // img2 이미지 위에 색깔을 그리기 위해 Element에 접근하는 data_output 포인터 변수

            if(data_input[y*img2.cols+x] == 0) {        // 현재 Element의 값이 0이면, 즉 검은색이면
                if(count == 0){                         // 그때의 count 값이 0이면, 파랑색
                data_output[y * img2.cols*3 + x*3] = 255;           // B
                data_output[y * img2.cols*3 + x*3 + 1] = 144;       // G
                data_output[y * img2.cols*3 + x*3 + 2] = 30;        // R
                } else if(count == 1) {                 // 그때의 count 값이 1이면, 초록색
                    data_output[y * img2.cols*3 + x*3] = 0;         // B
                    data_output[y * img2.cols*3 + x*3 + 1] = 128;   // G
                    data_output[y * img2.cols*3 + x*3 + 2] = 0;     // R
                }else if(count == 2) {                  // 그때의 count 값이 2이면, 빨강색
                    data_output[y * img2.cols*3 + x*3] = 0;         // B
                    data_output[y * img2.cols*3 + x*3 + 1] = 0;     // G
                    data_output[y * img2.cols*3 + x*3 + 2] = 255;   // R
                }

                if(data_input[y*img2.cols+x+1] == 255) {            // 다음 Element의 값이 255이면, 즉 흰색이면
                    if(count == 2)          // 그때의 count 값이 2라면
                        count = 0;          // 0으로 변경
                    else                    // 2가 아니라면
                        count++;            // count 값을 1만큼 증가
                }
            }else if(data_input[y*img2.cols+x] == 255) {            // 현재 Element의 값이 255이면, 즉 흰색이면 노랑색
                data_output[y * img2.cols*3 + x*3] = 0;             // B
                data_output[y * img2.cols*3 + x*3 + 1] = 255;       // G
                data_output[y * img2.cols*3 + x*3 + 2] = 255;       // R
            }
        }   
    }

    imshow("Result", img2);
    
    waitKey(0);

    return 0;
}
```

다음과 같은 이미지가 출력되었다면, 성공이다.

![Result](/assets/images/opencv/assignment/opencv-assign-9.png)

전체 코드를 보이면서 OpenCV 색상 채우기 과제를 마무리 짓겠다.

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
            minMaxLoc(dup_src, 0, 0, 0, &p);       // 우리는 위치값만 필요하므로 최대와 최솟값을 저장할 변수는 필요치 않음.
            peaks.push_back(p.y);       // 위치 값 중 y값만을 peaks에 담자. 실제로 가장 큰 Peak를 가지는 히스토그램의 y값이 먼저 담기므로, 실제로 히스토그램 위에 Line을 그릴 때는 가장 작은 Peak를 가지는 히스토그램부터 그려진다. (Stack)
            dup_src.at<float>(p.y) = 0;        // 필자는 단순히 최솟값으로서 0을 채택했다.

            for(int j=0; j<10; j++) {           // p.y의 주변 반경 10만큼을 0으로 채운다.
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

    vector<int> peaks;          // draw_Line Function 반환 값을 저장할 변수 선언
    vector<int>::iterator iter;
    
    double median;              // 중앙값을 저장할 변수 선언
    
    Mat img1 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_GRAYSCALE);
    Mat img2 = imread("/Users/hexk/Desktop/test1.jpg", IMREAD_COLOR);
    
    Mat b_hist;     // 히스토그램이 저장될 Mat 객체 생성
    Mat histImg;    // draw_histogram 반환값을 저장하기 위한 Mat 객체 생성
    Mat dst;        // threshold 처리 후 결과 이미지를 저장하기 위한 Mat 객체 생성

    calcHist(&img1, 1, 0, Mat(), b_hist, 1, &histSize, &histRange, uniform, accumulate);

    GaussianBlur(b_hist, b_hist, Size(9, 9), 0);        // 9x9 가우시안 필터 적용

    histImg = draw_Histogram(b_hist);
    
    peaks = draw_Line(b_hist, histImg);         // 반환 값을 담자.
    
    for(iter = peaks.begin(); iter != peaks.end(); iter++)
        cout<<*iter<<endl;

    median = (peaks.at((peaks.size()/2)-1) + peaks.at((peaks.size()/2)+1))/2;

    threshold(img1, dst, median, 255, THRESH_BINARY);
    
    imshow("p1", img1);
    imshow("p2", dst);
    
    uchar *data_input = dst.data;

    int count = 0;

    for (int y = 0; y < img2.rows; y++) {
        for (int x = 0; x < img2.cols-1; x++) {
            uchar *data_output = img2.data;     // img2 이미지 위에 색깔을 그리기 위해 Element에 접근하는 data_output 포인터 변수

            if(data_input[y*img2.cols+x] == 0) {        // 현재 Element의 값이 0이면, 즉 검은색이면
                if(count == 0){                         // 그때의 count 값이 0이면, 파랑색
                data_output[y * img2.cols*3 + x*3] = 255;           // B
                data_output[y * img2.cols*3 + x*3 + 1] = 144;       // G
                data_output[y * img2.cols*3 + x*3 + 2] = 30;        // R
                } else if(count == 1) {                 // 그때의 count 값이 1이면, 초록색
                    data_output[y * img2.cols*3 + x*3] = 0;         // B
                    data_output[y * img2.cols*3 + x*3 + 1] = 128;   // G
                    data_output[y * img2.cols*3 + x*3 + 2] = 0;     // R
                }else if(count == 2) {                  // 그때의 count 값이 2이면, 빨강색
                    data_output[y * img2.cols*3 + x*3] = 0;         // B
                    data_output[y * img2.cols*3 + x*3 + 1] = 0;     // G
                    data_output[y * img2.cols*3 + x*3 + 2] = 255;   // R
                }

                if(data_input[y*img2.cols+x+1] == 255) {            // 다음 Element의 값이 255이면, 즉 흰색이면
                    if(count == 2)          // 그때의 count 값이 2라면
                        count = 0;          // 0으로 변경
                    else                    // 2가 아니라면
                        count++;            // count 값을 1만큼 증가
                }
            }else if(data_input[y*img2.cols+x] == 255) {            // 현재 Element의 값이 255이면, 즉 흰색이면 노랑색
                data_output[y * img2.cols*3 + x*3] = 0;             // B
                data_output[y * img2.cols*3 + x*3 + 1] = 255;       // G
                data_output[y * img2.cols*3 + x*3 + 2] = 255;       // R
            }
        }   
    }

    imshow("Result", img2);
    
    waitKey(0);

    return 0;
}
```