---
title: "[JAVA] WAV 파일을 RAW Data 로 변환 및 저장하기 (Wav to Raw) - Step 2"

categories:
  - Java
tags: 
  - Java
  - Wav
  - Raw
  - ETRI
last_modified_at: 2021-08-21
---

## 목차

[Step 1. WAV 파일을 RAW Data 로 변환하기 미완성 (Wav to Raw)](https://jee00609.github.io/java/how-convert-wav-to-raw/)

[Step 2. WAV 파일을 RAW Data 로 변환 및 저장하기 완성! (Wav to Raw)](https://jee00609.github.io/java/how-convert-wav-to-raw2/)

## 서문

바로 1년전 ETRI 를 하면서 공부했었던 WAV 파일에 대해서 다시 공부를 하면서 어떤 부분에서 잘못 했었는지 알게되었다.

같은 WAV 파일이라도 샘플 당 주파수, 혹은 주파수에 따라 큰 차이가 있다는 것이다.

특히 내가 사용하고 싶은 ETRI API 는 [PCM 음성 파일 제작](https://aiopen.etri.re.kr/data/pcm%EC%9D%8C%EC%84%B1%ED%8C%8C%EC%9D%BC%EC%A0%9C%EC%9E%91.pdf) 과 같이 RAW 형식 파일로 조정할 때 특정한 형식이 존재했다.

즉 내가 만들어야 하는 RAW 파일 형식은 아래와 같았다.

   * 샘플링 주파수 : 16000
   * 모노
   * 인코딩 : Signed 16bit PCM
   * LittleEndian

## 코드

따라서 내가 만든 Wav To Raw Pcm 코드는 아래와 같다.

```java
public void SaveRaw(File file) throws UnsupportedAudioFileException {
	OutputStream output = null;
	
	try {
	
		//Example -> output = new FileOutputStream("src/main/resources/static/audio/test.raw");
		output = new FileOutputStream("Directory with Raw file that you make(Wav to Raw).raw");
	} 
	catch (FileNotFoundException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}

	try {
		//핵심 코드
		//core code
		output.write(formatWavToRaw(changeFormat(AudioToByte(file), FORMAT)));

		//Just Test Code
		//Can Delete
		System.out.print("Success");

	} catch (IOException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
}
```

## 결과

<figure class="align-center">
  <a href="/assets/images/2021-08-21-java-wav-to-raw.png"><img src="/assets/images/2021-08-21-java-wav-to-raw.png"></a>
  <figcaption>ETRI 발음 평가가 성공!</figcaption>
</figure>

<figure class="align-center">
  <a href="/assets/images/2021-08-21-java-wav-to-raw-success.png"><img src="/assets/images/2021-08-21-java-wav-to-raw-success.png"></a>
  <figcaption>잘 저장되어 있는 모습</figcaption>
</figure>


## 비고

[가장 큰 도움을 받은 사이트](https://stackoverflow.com/questions/60626467/how-do-i-convert-audio-from-one-format-to-wav-or-raw-in-java)

[프로젝트 전문 (Github)](https://github.com/jee00609/WavToRawPCM)