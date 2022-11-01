# Run jupyter notebook on a server




On server: Open tmux and
```
jupyter lab --no-browser --port=4242
```

Local:
```
sshpass -p YOUR_SUPERSECRET_PASSWORD ssh -Y -N -L localhost:4242:localhost:4242 SERVER_NAME & 
```

Then go to your browser:

http://localhost:4242/lab
