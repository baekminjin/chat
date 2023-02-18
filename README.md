미완성

2023.02.18
*바로 꺼지는 현상 해결*

ChatData에서  private String nickname;을 주목해야 한다.

오류에서 
    Process: com.example.chat, PID: 12260
    java.lang.NullPointerException: Attempt to invoke virtual method 'boolean java.lang.String.equals(java.lang.Object)' on a null object reference
        at com.example.chat.ChatAdapter.onBindViewHolder(ChatAdapter.java:66)
        at com.example.chat.ChatAdapter.onBindViewHolder(ChatAdapter.java:18)
라는 메시지가 나타남.
이는  String.equals()메소드를 수행하였는데 이 object가 null이기 때문에 문제가 된다는 것이다


if(chat.getNickname().equals(this.myNickName)) {  chat.getNickname()이 null을반환하고 있을 것으로 보여
getNickname의 메소드가 있는 ChatData 클래스를 보면
private String nickname;

public String getNickname() {
return nickname;
}

nickname 변수가 아무것도 설정이 안되어있고
nickname = ~~~~; 처럼 무언가 값이 설정이 되어야 null이 아니기 때문에
private String nickname; 를 private String nickname = "" ; 으로 변경하여 null이 아니라는 것을 설정하니 정상적으로 실행되었다.

*오류?*
한 기기에서 nick1 , 다른 기기로 nick2로 메시지를 보내면 보내는 자와 받는자의 메시지 정렬이 이상함. ( 보내는 자의 메시지가 오른쪽으로 정렬이지만 왼쪽으로 정렬되는 현상)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

2023.2.17
실행이 되다가
앱 실행시 갑자기 켜졌다가 바로 오류 메시지 없이 꺼지는 현상이 발생됨

if) 실행될 시
ChatActivity에서  private String nick = "nick1"; 을 nick1을 에뮬레이터로 먼저 실행한 뒤 *다른* 에뮬레이터를 이용해 nick2로 변경한 뒤 실행하면 서로 연결되어 채팅이 된다.

-> 처음 가입할 때 닉네임을 설정하기 때문에 그 닉네임을 이용해 연결한다?
