# R

## Enable X11 display connection on a remote server

- If you already have a session open and want to enable X11

You probably got an error like this:

```
Error in .External2(C_X11, d$display, d$width, d$height, d$pointsize,  :                                                                      
  unable to start device X11cairo
In addition: Warning message:
In (function (display = "", width, height, pointsize, gamma, bg,  :
  unable to open connection to X11 display ''
```

Your current session probably gives these:

```R
# old terminal
> capabilites()             # returns X11 = FALSE 
> Sys.getenv('DISPLAY')     # returns localhost:xx.0
localhost:12.0
> x11('localhost:12.0')     # returns error message
```

**Fix:** We will redirect the `DISPLAY` parameter in the current session to the value in the new connection

1) Start a new ssh connection:

```sh
# new terminal
ssh -Y login@remote.server
```

Find the value of `DISPLAY` in this new session

In bash:

```sh
# new terminal
$ echo $DISPLAY
localhost:13.0 # returns localhost:xx.0
```

OR in R:

```R
# new terminal
> Sys.getenv('DISPLAY')
localhost:13.0 # returns localhost:xx.0
```

In the original R terminal, set the `DISPLAY` parameter to the new connection value:

```
# old terminal
> Sys.setenv('DISPLAY' = 'localhost:13.0')
> x11('localhost:13.0')  # or x11() - both should work
```

**--> Long term solution**

If security settings allow you to do so, in ssh config file (`~/.ssh/config`)

```
ForwardX11Trusted yes
```

If not, set the value of `ForwardX11Timeout` to prevent `X11` to stop during a session if it's opened in the last 24 hours (1d).

```
ForwardX11Timeout 1d
```

[Source](https://stackoverflow.com/a/67487865/7870777)

___
