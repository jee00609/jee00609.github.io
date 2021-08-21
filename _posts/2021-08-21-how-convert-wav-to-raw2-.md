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
import java.io.BufferedInputStream;
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.util.Arrays;

import javax.sound.sampled.AudioFileFormat;
import javax.sound.sampled.AudioFormat;
import javax.sound.sampled.AudioInputStream;
import javax.sound.sampled.AudioSystem;
import javax.sound.sampled.UnsupportedAudioFileException;
import javax.validation.constraints.NotNull;

public class WavToRaw {

	private FileInputStream fstream = null;
	private byte[] audioBytes = new byte[1024];
	private byte[] buff = new byte[1024];
	private int read;

	public WavToRaw() {
		super();
		// TODO Auto-generated constructor stub
	}

	// 리니어 PCM 인코딩 및 지정된 파라미터를 가지는 AudioFormat를 구축합니다.
	// http://cris.joongbu.ac.kr/course/java/api/javax/sound/sampled/AudioFormat.html
	private static final AudioFormat FORMAT = new AudioFormat(
		16_000, // 16 kHz, sampleRate
		16, // 16 bits, sampleSizeInBits
		1, // Mono, int channels
		true, // Signed
		false // Little endian, True is BigEndian
	);

	//바이트 배열을 Raw 파일로 저장
	//Save byte array as Raw file
	public void SaveRaw(File file) throws UnsupportedAudioFileException {
		OutputStream output = null;

		try {
			output = new FileOutputStream("Please write here to save Raw file.raw");
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

		try {
			//핵심 코드
			//core code
			output.write(formatWavToRaw(changeFormat(AudioToByte(file), FORMAT)));

			//Can delete
			//Just Test Code
			System.out.print("Success");

		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

	//Wav 파일에서 헤더 제거
	//Strip the header from the WAV file
	public byte[] formatWavToRaw(@NotNull final byte[] audioFileContent) {
		return Arrays.copyOfRange(audioFileContent, 44, audioFileContent.length);
	}

	//기존의 Wav 파일(바이트 배열) 을 다른 형식의 Wav 형식 (바이트 배열) 로 변환
	//WAV to WAV (different audio format)
	public byte[] changeFormat(@NotNull final byte[] audioFileContent, @NotNull final AudioFormat audioFormat)
			throws IOException, UnsupportedAudioFileException {
		try (final AudioInputStream originalAudioStream = AudioSystem
				.getAudioInputStream(new ByteArrayInputStream(audioFileContent));
				final AudioInputStream formattedAudioStream = AudioSystem.getAudioInputStream(audioFormat,
						originalAudioStream);
				final AudioInputStream lengthAddedAudioStream = new AudioInputStream(formattedAudioStream, audioFormat,
						audioFileContent.length);
				final ByteArrayOutputStream convertedOutputStream = new ByteArrayOutputStream()) {
			AudioSystem.write(lengthAddedAudioStream, AudioFileFormat.Type.WAVE, convertedOutputStream);
			return convertedOutputStream.toByteArray();
		}
	}

	//기존의 wav 파일을 바이트 배열로 변환
	//Convert existing wav file to byte array
	public byte[] AudioToByte(File file) {
		try {
			File inFile = file;
			fstream = new FileInputStream(inFile);

			ByteArrayOutputStream out = new ByteArrayOutputStream();
			BufferedInputStream in = new BufferedInputStream(fstream);

			while ((read = in.read(buff)) > 0) {
				out.write(buff, 0, read);
			}
			out.flush();
			audioBytes = out.toByteArray();

			// Do something with the stream
		} catch (FileNotFoundException ex) {

		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return audioBytes;
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