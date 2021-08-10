---
title: "[Spring] 브라우저에서 녹음 및 다운 기능 구현 (Coding Record Voice in browser)"

categories:
  - Spring
tags: 
  - Spring
  - Record
last_modified_at: 2021-08-10
---

어쩌다 보니 졸업 작품 주제를 변경해야 할 것 같아 먼저 필요한 기능들을 모듈 프로젝트로 나누어 구현해보는 중이다.

분명 브라우저에서 녹음하고 저장하는 기능들이 많은데 이걸 직접 구현한 포스팅을 찾기 힘들어 외국 자료를 찾아 내가 원하는 방식으로 고쳐 포스팅한다.

## 목차

[1.소개](#소개)

[2.시연 영상](#시연-영상)

[3.주요 코드](#주요-코드)

[4.비고](#비고)

## 소개

[![시작 화면](https://raw.githubusercontent.com/jee00609/STS_WebAudioRecorder/master/src/main/resources/static/assets/img/WebAudioRecorder.PNG)](https://github.com/jee00609/STS_WebAudioRecorder/blob/master/src/main/resources/static/assets/img/WebAudioRecorder.PNG)

이 프로젝트는 [simple-web-audio-recorder-demo](https://github.com/addpipe/simple-web-audio-recorder-demo) 프로젝트의 코드를 변경하여 만든 프로젝트입니다.

해당 프로젝트는 녹음을 한 모든 파일들이 순서대로 화면에 출력되며, 이름을 클릭하여 저장하는 방식으로 구현되어 있습니다.

자세한 사항은 [실제 데모](https://addpipe.com/simple-web-audio-recorder-demo/)를 통하여 확인하실 수 있습니다.

**따라서 이 프로젝트에서는 가장 최신으로 녹음한 파일만 출력되며, 이름이 아닌 다운로드 버튼 형식을 통해 저장할 수 있도록 구현하였습니다.**

이클립스 기반 스프링 애플리케이션으로 브라우저에서 확인할 수 있도록 하였습니다.

[무료 부트스트랩 템플릿](https://startbootstrap.com/template/bare) 을 사용하여 브라우저 디자인을 구성하였습니다.

## 시연 영상

<iframe width="560" height="315" src="https://www.youtube.com/embed/HbJitnzClyo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 주요 코드

* index.jsp

```jsp
  <div class="container">
        <div class="text-center mt-5">
            <p>Convert recorded audio to:</p>
            <select id="encodingTypeSelect">
                <option value="wav">Waveform Audio (.wav)</option>
                <option value="mp3">MP3 (MPEG-1 Audio Layer III) (.mp3)</option>
                <option value="ogg">Ogg Vorbis (.ogg)</option>
            </select>
            <div id="controls">
                <button id="recordButton">Record</button>
                <button id="stopButton" disabled>Stop</button>
            </div>
            <div id="formats"></div>
            <pre>Log</pre>
            <pre id="log"></pre>

            <pre>Recordings</pre>
            <ol id="recordingsList"></ol>

        </div>
    </div>
```

* app.js

```js
function createDownloadLink(blob,encoding) {
	
	var url = URL.createObjectURL(blob);
	var au = document.createElement('audio');
	var li = document.createElement('li');
	var link = document.createElement('a');
	
	var recordingsList = document.getElementById("recordingsList");
	
	//최신 녹음만 뜨도록 하기 위해 노드리스트의 길이를 저장
	var nodelist = recordingsList.childNodes.length;
	
	//add controls to the <audio> element
	au.controls = true;
	au.src = url;

	//link the a element to the blob
	link.href = url;
	link.download = new Date().toISOString() + '.'+encoding;
	link.innerHTML = '<br/><button class="btn_download"><i class="fa fa-download"></i> Download</button>';
	
	//If you want to put the button aside
	//link.innerHTML = '<button class="btn"><i class="fa fa-download"></i> Download</button>';

	//add the new audio and a elements to the li element
	li.appendChild(au);
	li.appendChild(link);
	
	//만약 하나라도 녹음을 했을 시 최신의 녹음만 남도록 기존의 녹음을 삭제
	//If even one is recorded, the existing recording is deleted so that only the latest recording remains.
	if (nodelist ==1){
		recordingsList.removeChild(recordingsList.childNodes[0]); 
	}

	//최신의 녹음만 노드리스트에 제공 --> Only the latest recordings are provided in the node list
	//add the li element to the ordered list
	recordingsList.appendChild(li);
	
	//다시 한번 노드리스트의 길이를 저장
	//once again save the length of the nodelist
	nodelist = recordingsList.childNodes.length;

}
```

* styles.css

```css
.btn_download {
  background-color: DodgerBlue;
  border: none;
  color: white;
  padding: 12px 30px;
  cursor: pointer;
  font-size: 20px;
}

/* Darker background on mouse-over */
.btn_download:hover {
  background-color: RoyalBlue;
}
```

## 비고

[프로젝트 전문](https://github.com/jee00609/STS_WebAudioRecorder)