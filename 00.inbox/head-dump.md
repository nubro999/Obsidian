# 파일 다운로드 (예시)
wget http://target.site/api/memory-dump

# 파일 타입 확인
file memory-dump

# 사람이 읽을 수 있는 문자열 추출
strings memory-dump | grep -E 'FLAG|CTF|flag'

# 앞부분만 확인
head memory-dump

# HEX로 확인
xxd memory-dump | head


GET http://verbal-sleep.picoctf.net:61913/heapdump 여기에서 dump파일 다운받아서 서치함