# C++ Setting

Windows 11에서 VS Code와 MSYS2 UCRT64의 GCC를 사용하는 C++17 설정입니다. `bits/stdc++.h`를 지원하며, 현재 열어둔 C++ 파일을 단축키로 컴파일하고 실행합니다.

## 준비

이미 아래 준비를 마쳤다면 바로 사용 방법으로 넘어가세요.

1. [MSYS2](https://www.msys2.org/)를 기본 경로인 `C:\msys64`에 설치합니다.
2. **MSYS2 UCRT64** 터미널에서 다음 명령으로 컴파일러와 디버거를 설치합니다.

   ```bash
   pacman -S --needed mingw-w64-ucrt-x86_64-toolchain
   ```

   패키지 선택에는 Enter를, 설치 확인에는 Y를 입력합니다.

3. Windows의 사용자 `Path` 환경 변수에 `C:\msys64\ucrt64\bin`을 추가합니다.
4. VS Code에 Microsoft의 **C/C++** 확장을 설치하고, VS Code 창을 모두 닫았다가 다시 엽니다.

## 사용 방법

1. 저장소 상단의 **Code → Download ZIP**을 누르고, 다운로드한 ZIP을 압축 해제합니다.
2. VS Code에서 **File → Open Folder**로 `README.md`, `main.cpp`, `.vscode`가 함께 들어 있는 폴더를 엽니다. ZIP 안에서 직접 열거나 `.vscode` 폴더만 열지 않습니다.
3. `main.cpp`를 열고 **Ctrl + S**로 저장합니다.
4. **Ctrl + F5**를 누릅니다. 실행 설정 선택창이 나오면 **Run C++**를 선택합니다.
5. 아래쪽 **Terminal**을 클릭하고 `3 5`를 입력한 뒤 Enter를 누릅니다. 예제의 예상 출력은 `8`입니다.

`A.cpp`, `B.cpp`처럼 새 파일을 만들어도 실행할 파일의 탭을 선택하고 저장한 뒤 **Ctrl + F5**를 누르면 됩니다. 실행 파일은 소스와 같은 폴더에 만들어집니다. 각 소스 파일은 독립적인 `main` 함수를 가진 단일 파일 프로그램으로 사용합니다.

| 단축키 | 기능 |
| --- | --- |
| Ctrl + F5 | 현재 C++ 파일 컴파일 후 실행 |
| Ctrl + Shift + B | 현재 C++ 파일 컴파일만 수행 |
| F5 | 현재 C++ 파일 컴파일 후 디버깅 |
| Shift + F5 | 실행 또는 디버깅 중지 |

입력은 **Debug Console**이 아닌 **Terminal**에 넣습니다. 컴파일 오류가 있으면 실행을 중단하도록 설정하여 이전 실행 파일이 실수로 실행되는 것을 막습니다.

## 설정

| 파일 | 역할 |
| --- | --- |
| `.vscode/tasks.json` | GCC 경로와 컴파일 옵션 |
| `.vscode/launch.json` | 실행 및 GDB 경로 |
| `.vscode/c_cpp_properties.json` | 자동완성, 헤더 인식, C++ 표준 |
| `.vscode/settings.json` | 컴파일 오류 발생 시 실행 중단 |
| `.vscode/extensions.json` | Microsoft C/C++ 확장 추천 |

컴파일 옵션은 `-std=gnu++17 -O2 -g -Wall -Wextra`입니다. `-O2` 최적화 때문에 디버깅 중 일부 변수나 실행 줄이 예상과 다르게 보일 수 있습니다. 단계별 디버깅이 필요하면 `tasks.json`의 `-O2`를 `-Og`로 변경하세요.

MSYS2를 다른 위치에 설치했다면 위 설정에 있는 컴파일러·디버거 경로와 Windows `Path`를 실제 설치 위치에 맞춥니다. 헤더에 빨간 밑줄이 보이면 Microsoft C/C++ 확장의 설치 여부와 `compilerPath`를 확인하세요.

대회 채점 서버의 컴파일러 버전과 C++ 표준은 대회 공지를 따릅니다. C++ 표준을 바꾸려면 `tasks.json`의 `-std` 옵션과 `c_cpp_properties.json`의 `cppStandard`를 함께 변경하세요. DOMjudge에는 문제의 `.cpp` 소스를 제출합니다.

## 참고

- [VS Code 공식 MinGW 설정 안내](https://code.visualstudio.com/docs/cpp/config-mingw)
- [MSYS2 공식 설치 안내](https://www.msys2.org/)
