Mac OSX Notes
=============

### Security
https://github.com/drduh/macOS-Security-and-Privacy-Guide - A fantastic resource!

### Prevent Photos app from opening when SD card is inserted
    defaults -currentHost write com.apple.ImageCapture disableHotPlug -bool YES

### Mac version of `shred` - secure deletion tool
    alias shred=/usr/bin/srm

### Bash replacement for `cpulimit` tool
Allows you to limit the amount of CPU time a process can use.

    function cpulimit () {
      PID=$1
      REST_TIME=${2}
      REST_TIME=${REST_TIME:=1.5}
      RUN_TIME=${3}
      RUN_TIME=${RUN_TIME:=1}
      echo -n "Starting: $(date) pid=$PID rest=${REST_TIME} run=${RUN_TIME}."
      if [ "$PID" ];then
        while true;do
          kill -SIGSTOP ${PID}
          sleep ${REST_TIME}
          kill -SIGCONT ${PID}
          sleep ${RUN_TIME}
          echo -n .
        done
        date
      else
        echo "ERROR: must supply pid."
        echo "USAGE: $0 pid <rest-time> <run-time>"
      fi
    }

Usage: `cpulimit <PID> <WAIT_TIME> <RUN_TIME>`  (only the PID is required)

### Combine multiple files into a single PDF
* https://forums.adobe.com/message/6788486#6788486

### [Cannot erase USB flash drive, "name invalid"](https://discussions.apple.com/message/29454263#message29454263)
The GUI Disk Utility refuses to format my 16 GB Sandisk Cruzer USB Stick.

    diskutil eraseVolume HFS+ NAME disk2

### License

WTFPL - See [LICENSE](https://github.com/jonathancross/jc-docs/blob/master/LICENSE) for more info.
