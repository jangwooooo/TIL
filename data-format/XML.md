# XML

## XML이란

- XML은 EXtensible Markup Language의 약자이다.
- 수많은 응용 분야에서 데이터를 저장하고 전달하는 중요한 역할을 맡고 있습니다.
- HTML과 매우 비슷한 문자 기반의 마크업 언어(text-based markup language)이다.
- 그러나 XML은 HTML처럼 데이터를 보여주는 목적이 아닌, 데이터를 저장하고 전달할 목적으로만 만들어졌다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<programming_languages>
    <language>
        <name>HTML</name>
        <category>web</category>
        <developer>W3C</developer>
        <version status="working draft">5.1</version>
        <priority rating="1">high</priority>
    </language>
</programming_languages>
```

<hr>

## XML 특징

- 다목적 마크업 언어
- 데이터를 손쉽게 교환 가능
- 확장성이 좋음
- 데이터를 전달하고 저장하는 것만을 목적으로 함
- 유니코드 문자로만 이루어짐

<hr>

## XML 사용예시

- XML은 대표적으로 sitemap.xml에 쓰인다.
- sitemap.xml
  - 사이트가 매우 크거나 서로 링크가 종속적으로 연결되지 않은 경우 크롤러가 일부 페이지를 누락하는 일이 있는데 이를 방지한다.
