# Program do sterowania robotem tpyu line follower

## współpracuje z programem z repozytorium 
https://github.com/Kneicik/Line_followerV0

Należy zmienić port do wysyłania ramek w robocie na 5005 zamiast 1234:

  if(udp.listen(5005)) {
      Serial.print("UDP Listening on IP: ");
      Serial.println(WiFi.localIP());
  }