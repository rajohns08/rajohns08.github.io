---
layout: post
title: Show Loading Dots in Bash Script
---

I was recently working on a bash script where I wanted to show loading dots to give some indication to the user that a process was still working. After googling I pieced together a simple function I'd like to share in case anyone else is looking for this in any of their bash scripts.

```bash
doSomeTask() {
  // make build or some other long task
}

showLoading() {
  mypid=$!
  loadingText=$1

  echo -ne "$loadingText\r"

  while kill -0 $mypid 2>/dev/null; do
    echo -ne "$loadingText.\r"
    sleep 0.5
    echo -ne "$loadingText..\r"
    sleep 0.5
    echo -ne "$loadingText...\r"
    sleep 0.5
    echo -ne "\r\033[K"
    echo -ne "$loadingText\r"
    sleep 0.5
  done

  echo "$loadingText...FINISHED"
}

doSomeTask & showLoading "DOING SOME TASK"
```

The ampersand in the function call is a little misleading as it seems to be an "AND" syntax. This strange syntax works well though because the ampersand actually tells the preceding function call to run in the background asynchronously. The `showLoading` function prevents any subsequent commands from executing, however, because it runs in a while loop until the previous function pid is finished executing. The `-n` echo option says don't print new line character at end of echo. The `-e` option says to interpret `\r` as carriage return. The `\r` carriage return basically says move the cursor to the beginning of the line. Finally, the `\r\033[K` says to move the cursor to the beginning of the line AND clear the current line.
