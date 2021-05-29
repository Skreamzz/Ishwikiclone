# Running a Python web server
This works surprisingly well and you can use this to host your static html page
1. Run `apk update`
2. Run `apk add python3`
3. Create an index.html file in the directory you chose
`cd <your directory>`
`touch index.html`
4. Edit `index.html` and write whatever you want inside of the file.
5. Run `python3 -m http.server`
6. Navigate to `http://127.0.0.1:8000` if you want to view the website on your device (localhost)
7. From any other device on your network, navigate to `http://<your device's private ip>:8000`