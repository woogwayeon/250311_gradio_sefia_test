# 250311_gradio_sefia_test
그라디오를 사용해서 인터페이스를 만들고, 이미지에 세피아 필터를 적용시켜보았습니다!

## 이미지 필터 프로그램

```python
import numpy as np
import gradio as gr

def sepia(inputImg):
    sepia = np.array([
        [0.393, 0.769, 0.189],
        [0.349, 0.686, 0.168],
        [0.272, 0.534, 0.131]
    ])

    sepiaImg = inputImg.dot(sepia.T)
    sepiaImg /= sepiaImg.max()

    return sepiaImg

demo = gr.Interface(fn=sepia, inputs="image", outputs="image")
demo.launch(debug=True, share=True)
```

전반적인 코드는 위와 똑같다!

`sepia()`라는 함수에 인자로 `inputImg` 를 받는다

그 필터는 array로 넣어준다!

`inputImg` (이미지 배열)이랑 `sepia.T` (세피아 필터 행렬)을 `dot()` 연산으로 곱해줌!

`sepia.T`는 즉 원래 `sepia` 행렬의 행과 열을 바꾼것이 됨 ㅇㅇ

다음 `sepiaImg`의 모든 값을 `sepiaImg.max()`로 나눠 정규화한다!  → 값을 **0-1 사이**로 조정함

(근데 이거 `sepiaImg.max()`가 0일때 못나누는 이슈가 생길 수 있으니 수정해주는게 좋겠다,.)

암튼 그 다음 똑같이 `gr.Interface(실행할 함수, 입력할거=이미지, 출력할거=이미지)`

써서 UI만듦!

디버깅모드랑 공유링크 on도 해주면 완료이다!
