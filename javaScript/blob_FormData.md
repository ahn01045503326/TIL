## File 리스트(Blob 객체 리스트)를 FormData에 넣어서 한번에 전송하기

---

### 1. 프론트에서 이미지 파일 한번에 post로 전송 
````
[javascript]

const formData = new FormData();
const blobList = [blob1, blob2, blob3]; // 전송할 Blob 객체 리스트

// Blob 객체 리스트를 FormData에 추가
blobList.forEach((blob, index) => {
  formData.append(`blob${index}`, blob);
});

// FormData를 전송
const xhr = new XMLHttpRequest();
xhr.open('POST', '/upload');
xhr.send(formData);
````
- 위 코드에서는 blobList 변수에 전송할 Blob 객체 리스트를 할당한 후, forEach() 메서드를 사용하여 Blob 객체 리스트를 순회하면서 FormData에 추가하고 있습니다. 이 때, append() 메서드의 첫 번째 인자로는 Blob 객체를 구분하기 위한 이름을 지정하고, 두 번째 인자로는 Blob 객체를 전달하고 있습니다.
- 마지막으로, xhr.send(formData) 코드를 사용하여 FormData를 전송하고 있습니다. 이렇게 전송된 데이터는 서버에서 FormData로 받아 처리할 수 있습니다.

---
<br>

### 2. controller에서 이미지파일 받아서 처리
````
[java]

import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.multipart.MultipartHttpServletRequest;
import org.springframework.web.multipart.MultipartFile;

@RestController
public class FileUploadController {
    @PostMapping("/upload")
    public String handleFileUpload(MultipartHttpServletRequest request) {
        // 파일 처리 작업 수행
        for (MultipartFile file : request.getFiles("blob")) {
            System.out.println("File uploaded: " + file.getOriginalFilename());
            // 파일 처리 작업 수행
        }
        return "File uploaded!";
    }
}
````
- 위 코드에서는 MultipartHttpServletRequest 인터페이스를 사용하여 FormData에 포함된 파일 정보를 받아옵니다. 이 때, getFiles() 메서드를 사용하여 blob 필드에서 업로드된 파일 리스트를 받아옵니다.
- 파일 처리 작업은 for문 내에서 수행하면 됩니다. 이 때, file 객체를 사용하여 파일 정보를 받아올 수 있습니다.
- 마지막으로, File uploaded! 문자열을 반환하여 업로드 완료를 알리고 있습니다. 이 문자열은 클라이언트 측에서 받아서 처리할 수 있습니다.