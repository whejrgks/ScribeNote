# Pdf 텍스트 추출 프로그램 개발
_Exported on 12/10/2025 at 10:46:12 GMT+9 from Cursor (2.1.50)_

---

**User**

@C:\DEV\Cursor_pro\ScribeNote/repository/pdfs 폴더에있는PDF 파일들의텍스트를추출하는프로그램을만들어줘.

---

**Cursor**


PDF 텍스트 추출 프로그램을 만들기 위해 폴더 구조를 확인 중입니다.



PDF 텍스트 추출 프로그램 작성 중입니다. Python과 PDF 라이브러리를 사용합니다.


```python
"""
PDF 텍스트 추출 프로그램
repository/pdfs 폴더에 있는 모든 PDF 파일에서 텍스트를 추출합니다.
"""

import os
from pathlib import Path
from pypdf import PdfReader
import sys


def extract_text_from_pdf(pdf_path):
    """
    PDF 파일에서 텍스트를 추출합니다.
    
    Args:
        pdf_path: PDF 파일 경로
        
    Returns:
        추출된 텍스트 문자열
    """
    try:
        reader = PdfReader(pdf_path)
        text = ""
        
        print(f"처리 중: {os.path.basename(pdf_path)} ({len(reader.pages)} 페이지)")
        
        for page_num, page in enumerate(reader.pages, 1):
            page_text = page.extract_text()
            text += f"\n--- 페이지 {page_num} ---\n"
            text += page_text
            text += "\n"
        
        return text
    except Exception as e:
        print(f"오류 발생 ({pdf_path}): {str(e)}")
        return None


def save_text_to_file(text, output_path):
    """
    추출된 텍스트를 파일로 저장합니다.
    
    Args:
        text: 저장할 텍스트
        output_path: 출력 파일 경로
    """
    try:
        os.makedirs(os.path.dirname(output_path), exist_ok=True)
        with open(output_path, 'w', encoding='utf-8') as f:
            f.write(text)
        print(f"저장 완료: {output_path}")
    except Exception as e:
        print(f"파일 저장 오류 ({output_path}): {str(e)}")


def main():
    """메인 함수"""
    # PDF 폴더 경로
    pdf_folder = Path("repository/pdfs")
    output_folder = Path("repository/extracted_texts")
    
    # 폴더가 존재하는지 확인
    if not pdf_folder.exists():
        print(f"오류: PDF 폴더를 찾을 수 없습니다: {pdf_folder}")
        sys.exit(1)
    
    # PDF 파일 목록 가져오기
    pdf_files = list(pdf_folder.glob("*.pdf"))
    
    if not pdf_files:
        print(f"PDF 파일을 찾을 수 없습니다: {pdf_folder}")
        sys.exit(1)
    
    print(f"\n총 {len(pdf_files)}개의 PDF 파일을 찾았습니다.\n")
    print("=" * 60)
    
    # 각 PDF 파일 처리
    for pdf_file in pdf_files:
        print(f"\n파일: {pdf_file.name}")
        print("-" * 60)
        
        # 텍스트 추출
        extracted_text = extract_text_from_pdf(pdf_file)
        
        if extracted_text:
            # 출력 파일 경로 생성
            output_file = output_folder / f"{pdf_file.stem}.txt"
            
            # 텍스트 저장
            save_text_to_file(extracted_text, output_file)
        else:
            print(f"텍스트 추출 실패: {pdf_file.name}")
    
    print("\n" + "=" * 60)
    print(f"\n모든 작업이 완료되었습니다!")
    print(f"추출된 텍스트는 '{output_folder}' 폴더에 저장되었습니다.")


if __name__ == "__main__":
    main()

```

```pip-requirements
pypdf>=3.17.0

```

```markdown
# PDF 텍스트 추출 프로그램

이 프로그램은 `repository/pdfs` 폴더에 있는 모든 PDF 파일에서 텍스트를 추출합니다.

## 설치 방법

1. 필요한 패키지 설치:
```bash
pip install -r requirements.txt
```

## 사용 방법

프로그램 실행:
```bash
python extract_pdf_text.py
```

## 출력

추출된 텍스트는 `repository/extracted_texts` 폴더에 각 PDF 파일명과 동일한 이름의 `.txt` 파일로 저장됩니다.

## 기능

- PDF 폴더의 모든 PDF 파일 자동 감지
- 각 페이지별로 텍스트 추출
- UTF-8 인코딩으로 텍스트 파일 저장
- 진행 상황 및 오류 메시지 출력

```


PDF 텍스트 추출 프로그램을 생성했습니다.

## 생성된 파일들:

1. **`extract_pdf_text.py`** - 메인 프로그램
   - `repository/pdfs` 폴더의 모든 PDF 파일을 자동으로 찾아서 처리
   - 각 PDF에서 텍스트 추출
   - `repository/extracted_texts` 폴더에 `.txt` 파일로 저장

2. **`requirements.txt`** - 필요한 패키지 목록
   - `pypdf` 라이브러리 포함

3. **`README.md`** - 사용 설명서

## 사용 방법:

1. 패키지 설치:
   ```bash
   pip install -r requirements.txt
   ```

2. 프로그램 실행:
   ```bash
   python extract_pdf_text.py
   ```

프로그램은 5개의 PDF 파일을 처리하고, 각 파일의 텍스트를 개별 `.txt` 파일로 저장합니다. 진행 상황과 결과가 콘솔에 출력됩니다.

실행할까요?

```shellscript
   pip install -r requirements.txt
```

```shellscript
   python extract_pdf_text.py
```

---

**User**

지금까지작업된내용을Report 폴더에마크다운파일로저장해줘.

---

**Cursor**


작업 내용을 Report 폴더에 마크다운 파일로 저장 중입니다.



작업 내용을 Report 폴더에 마크다운 파일로 저장 중입니다.


```markdown
# PDF 텍스트 추출 프로그램 개발 리포트

## 작업 개요

`repository/pdfs` 폴더에 있는 PDF 파일들의 텍스트를 추출하는 프로그램을 개발했습니다.

## 작업 일시

2024년 (작업 완료 시점)

## 작업 내용

### 1. 프로그램 개발

PDF 파일에서 텍스트를 추출하는 Python 프로그램을 개발했습니다.

#### 주요 기능
- `repository/pdfs` 폴더의 모든 PDF 파일 자동 감지
- 각 PDF 파일의 모든 페이지에서 텍스트 추출
- 페이지별로 구분하여 텍스트 저장
- 추출된 텍스트를 `repository/extracted_texts` 폴더에 `.txt` 파일로 저장
- UTF-8 인코딩 지원
- 진행 상황 및 오류 메시지 출력

### 2. 생성된 파일 목록

#### `extract_pdf_text.py`
메인 프로그램 파일로, 다음 기능을 포함합니다:

- `extract_text_from_pdf(pdf_path)`: PDF 파일에서 텍스트를 추출하는 함수
- `save_text_to_file(text, output_path)`: 추출된 텍스트를 파일로 저장하는 함수
- `main()`: 프로그램의 메인 실행 함수

**주요 코드 구조:**
```python
import os
from pathlib import Path
from pypdf import PdfReader
import sys
```

#### `requirements.txt`
프로그램 실행에 필요한 패키지 목록:
```
pypdf>=3.17.0
```

#### `README.md`
프로그램 사용 방법 및 설명서

### 3. 처리 대상 PDF 파일

다음 5개의 PDF 파일이 `repository/pdfs` 폴더에 있습니다:

1. `Attention Is All You Need-1706.03762v7.pdf`
2. `Efficient Estimation of Word Representations in-1301.3781v3.pdf`
3. `Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks-2005.11401v4.pdf`
4. `Training language models to follow instructions-2203.02155v1.pdf`
5. `Universal Language Model Fine-tuning for Text Classification-1801.06146v5.pdf`

## 사용 방법

### 1. 패키지 설치
```bash
pip install -r requirements.txt
```

### 2. 프로그램 실행
```bash
python extract_pdf_text.py
```

### 3. 출력 결과
- 추출된 텍스트는 `repository/extracted_texts` 폴더에 저장됩니다.
- 각 PDF 파일명과 동일한 이름의 `.txt` 파일로 저장됩니다.
- 예: `Attention Is All You Need-1706.03762v7.txt`

## 프로그램 상세 설명

### 함수별 설명

#### `extract_text_from_pdf(pdf_path)`
- **기능**: PDF 파일에서 텍스트를 추출
- **입력**: PDF 파일 경로
- **출력**: 추출된 텍스트 문자열 (페이지별로 구분)
- **오류 처리**: 예외 발생 시 오류 메시지 출력 및 None 반환

#### `save_text_to_file(text, output_path)`
- **기능**: 추출된 텍스트를 파일로 저장
- **입력**: 텍스트 문자열, 출력 파일 경로
- **특징**: 출력 폴더가 없으면 자동 생성, UTF-8 인코딩 사용

#### `main()`
- **기능**: 프로그램의 메인 실행 로직
- **처리 과정**:
  1. PDF 폴더 존재 여부 확인
  2. PDF 파일 목록 수집
  3. 각 PDF 파일에 대해 텍스트 추출 및 저장
  4. 진행 상황 출력

## 기술 스택

- **언어**: Python
- **주요 라이브러리**: 
  - `pypdf` (v3.17.0 이상): PDF 파일 읽기 및 텍스트 추출
  - `pathlib`: 경로 처리
  - `os`: 파일 시스템 작업

## 프로그램 특징

1. **자동화**: 폴더 내 모든 PDF 파일을 자동으로 처리
2. **안정성**: 오류 처리 및 예외 상황 대응
3. **사용자 친화적**: 진행 상황 및 결과를 명확하게 출력
4. **유연성**: 페이지별로 텍스트를 구분하여 저장

## 향후 개선 가능 사항

- PDF 이미지에서 OCR을 통한 텍스트 추출 기능 추가
- 다양한 PDF 형식 지원 강화
- 추출된 텍스트의 전처리 옵션 추가 (예: 불필요한 공백 제거)
- 배치 처리 옵션 추가
- 진행률 표시 기능 개선

## 완료 상태

✅ PDF 텍스트 추출 프로그램 개발 완료
✅ requirements.txt 파일 생성 완료
✅ README.md 문서 작성 완료
✅ 작업 리포트 작성 완료

```


작업 내용을 `Report/작업_리포트.md` 파일로 저장했습니다.

리포트에는 다음 내용이 포함되어 있습니다:

- 작업 개요 및 목적
- 생성된 파일 목록 및 설명
- 처리 대상 PDF 파일 목록
- 사용 방법
- 프로그램 상세 설명 (함수별 설명)
- 기술 스택
- 프로그램 특징
- 향후 개선 가능 사항

리포트는 마크다운 형식으로 작성되어 있으며, `Report` 폴더에 저장되었습니다.

