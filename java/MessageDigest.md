# MessageDigest
> - 여러가지 key를 합하여 중복되지 않은 Primary key를 만들때 사용할 수 있음
> - 문자열이 같은지 확인할때 MD값으로 변경하여 비교할 수 있음
> - 파일이 같은지 확인할때 MD값으로 변경하여 비교할 수 있음

---

#### Code

````
[ MDUtil.java ]

public class MDUtil {
	
    public String encrypt(String text) throws NoSuchAlgorithmException {
        MessageDigest md = MessageDigest.getInstance("SHA-256");
        md.update(text.getBytes());

        return bytesToHex(md.digest());
    }

    private String bytesToHex(byte[] bytes) {
        StringBuilder builder = new StringBuilder();
        for (byte b : bytes) {
            builder.append(String.format("%02x", b));
        }
        return builder.toString();
    }

}
````