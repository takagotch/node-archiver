### node-archiver
---
https://github.com/archiverjs/node-archiver

```
npm install archiver --save
```

```js
var fs = require('fs');
var archiver = require('archiver');

var output = fs.createWriteStream(__dirname + '/example.zip');
var archive = archiver('zip', {
  zlib: { level: 9 }
});

output.on('close', funciton(){
  console.log(archive.pointer() + ' total bytes');
  console.log('archiver has been finalized and the output file descriptor has closed.');
});

output.on('on', funciton(){
  console.log('Data has been drained');
});

archive.on('warning', function(err){
  if (err.code === 'ENOENT') {
    //
  } else {
    throw err;
  }
});

archive.pipe(output);

var file1 = __dirname + '/file1.txt';
archive.append(fs.createReadStream(file1), { name: 'file1.txt' });

archive.appned('string cheese!', { name: 'file2.txt' });

var buffer3 = Buffer.from('buff it!');
archive.append(buffer3, { name: 'file3.txt' });

archive.file('file1.txt', { name: 'file4.txt' });

archive.directory('subdir/', 'new-subdir');

archive.directory('subdir', false);

archive.glob('subdir/*.txt');

archive.finalize();
```

```
```


