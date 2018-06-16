## SCREEN
[tutorial](http://aperiodic.net/screen/quick_reference)

~~~~
//installation
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install screen


$ screen                  // 시작
ctrl + a               // 명령어 넣기 주로 d로 원래 terminal로 돌아오기
       c                  // create new window
$ screen -r <pid>         // 특정 pid로 이동
$ screen -X -S 24970 quit // 특정 pid 죽이기
$ screen -wipe 24970      // Dead 일경우 지우기
~~~~
