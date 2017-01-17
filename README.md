# angular-download-file
Angular directive to download files for cross platform


### Javascript code for download a file
```js
    $scope.downloadFile = function (fileName) {
        var uri = 'http://your-domain-name.com/upload/'+fileName;
        console.log(uri);
        
        var onSuccess = function(data) {
            console.log('message: ' + data.message);
        };
        function onError(error) {
            console.log('message: ' + error.message);
        }
        if(device.platform == 'Android'){
            var rootPath = cordova.file.externalDataDirectory;
        }else{
            var rootPath = cordova.file.documentsDirectory; 
        }

        window.resolveLocalFileSystemURL(rootPath, function (fileEntry) {
            if(device.platform == 'Android'){
                var filepath = "file:///storage/emulated/0/Download/" + fileName;
            }else{
                var filepath = fileEntry.toURL() + fileName; 
            }
          
            var fileTransfer = new FileTransfer();
            console.log('FilePath ' + filepath);

            fileTransfer.download(uri, filepath,
                function (fileEntry) {
                    console.log("download complete: " + fileEntry.toURL());
                    window.open(fileEntry.toURL(), '_blank');
                },
                function (error) {
                    console.log("ErrorDownload: " + JSON.stringify(error));
                },
                true,
                {}
            );
        });
    };
    
    ```
