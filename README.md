### assemble
---
https://github.com/assemble/assemble/

```
npm install -D asemble
npm run build
npm install --global assemble
assemble
assemble foo
assemble foo bar
assemble --cwd=docs
assemble --emit=view
assemble --foo
assemble --foo=bar
assemble --option=foo
assemble --option=foo:bar
assemble --option.foo.bar.baz=qux
```

```
{
  "scripts": {
    "build": "assemble"
  }
}
```

```js
var assemble = require('assemble');
var app = assemble();

app.create('includes', {viewType: 'partial'});

app.include('foo.md', {contents: new Buffer('this is contents')});

app.includes({
  path: 'foo.md', contents: new Buffer('this is contents'),
  path: 'bar.md', contents: new Buffer('this is contents'),
  path: 'baz.md', contents: new Buffer('this is contents')
});
app.includes('*.{md,hbs}', {cwd: 'templates/includes'});

app.create('snippet', {viewType: 'partial'});

app.create('snippet');
app.snippets.option('viewType', ['partial']);

app.engine(ext, fn);

app.engine('hbs', require('engine-handlebars'));
app.engine('txt', function(str, locals, cb){
  cb(null, str);
});

app.option('engine', 'hbs');

app.src('templates/*.*')
  .pipe(app.renderFile('hbs'))

app.render(view, {title: 'Foo'}, function(err, view){
});

app.src('src/*.hbs');
app.src('src/*.hbs', { layout: 'default' });

app.dest('dist/');

app.task('assets', function(){
  return app.copy('assets/**', 'dist/');
});

app.src('*hbs')
  .pipe(app.renderfile())
  .pipe(app.dest('foo'));
  
app.engine('txt', function(src, locals, cb){
  cb(null, str);
});
app.src('*.hbs')
  .pipe(app.renderfile('txt'))
  .pipe(app.dest('foo'));

app.task('default', function(){
  app.src('templates/*.hbs')
    .pipe(app.dest('site/'));
});

app.build(['foo', 'bar'], function(err){
  if(err) throw err;
  console.log('done!');
});

app.task('watch', function(){
  app.watch('docs/*.md', ['docs']);
});
```


