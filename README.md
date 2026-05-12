yaml
name: Build ChineseStrokeIME

on:
  push:
    branches: [ "main", "master" ]
  workflow_dispatch:

jobs:
  build:
    runs-on: windows-latest

    steps:
    - uses: actions/checkout@v4

    - name: Install MinGW
      run: |
        choco install mingw -y
        echo "C:\ProgramData\chocolatey\lib\mingw\tools\mingw64\bin" >> $env:GITHUB_PATH

    - name: Build
      run: |
        mingw32-make clean
        mingw32-make

    - name: Upload EXE
      uses: actions/upload-artifact@v4
      with:
        name: ChineseStrokeIME
        path: ChineseStrokeIME.exe
