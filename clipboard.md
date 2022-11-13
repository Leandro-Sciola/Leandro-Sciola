# Clipboard

### esbuild-linux-32

package.json

```json
{
  "name": "esbuild-linux-32",
  "version": "0.15.6",
  "description": "The Linux 32-bit binary for esbuild, a JavaScript bundler.",
  "repository": "https://github.com/evanw/esbuild",
  "license": "MIT",
  "preferUnplugged": false,
  "engines": {
    "node": ">=12"
  },
  "os": [
    "linux"
  ],
  "cpu": [
    "ia32"
  ]
}
```

package.json

```json
{
  "name": "sciola",
  "dependencies": {
    "@ericblade/quagga2": "^1.7.6",
    "@fortawesome/fontawesome-free": "^6.2.0",
    "assert": "^2.0.0",
    "axios": "^1.1.3",
    "bootbox": "^5.5.3",
    "bootstrap": "^5.2.2",
    "chart.js": "^3.9.1",
    "cors": "^2.8.5",
    "express": "^4.18.1",
    "express-http-proxy": "^1.6.3",
    "express-status-monitor": "^1.3.4",
    "fs": "0.0.1-security",
    "glob": "^8.0.3",
    "helmet": "^5.1.0",
    "highlight.js": "^11.5.1",
    "jquery": "^3.6.1",
    "js-yaml": "^4.1.0",
    "magic-globals": "^0.9.1",
    "mariadb": "^3.0.0",
    "md5": "^2.3.0",
    "module-alias": "^2.2.2",
    "mongojs": "^3.1.0",
    "mysql2": "^2.3.3",
    "path": "^0.12.7",
    "pg": "^8.7.3",
    "pg-hstore": "^2.3.4",
    "portfinder": "^1.0.28",
    "prismjs": "^1.28.0",
    "qunit": "^2.19.1",
    "react": "^18.2.0",
    "request": "^2.88.0",
    "require-dir": "^1.2.0",
    "rimraf": "^3.0.2",
    "runtime-memcache": "^2.1.1",
    "sass": "^1.52.3",
    "sequelize": "^6.20.1",
    "string": "^3.3.3",
    "tabulator-tables": "^5.4.2",
    "terser": "^5.14.1",
    "twig": "^1.15.4",
    "util": "^0.12.4",
    "validator": "^13.7.0",
    "vue": "^3.2.37",
    "xml-parser": "^1.2.1"
  }
}
```

```twig
--------------------------------------------------------------------------------
Include multiple JS files via Twig.

<script type="text/javascript">
var arr = [];
{% for file in js %}
    arr.push("{{ file }}");
{% endfor %}
$_["file"].include(arr);
</script>
--------------------------------------------------------------------------------
```

```js
--------------------------------------------------------------------------------
const twig = require("twig");
Object.keys(mvc.view.functions).forEach(name => {
    twig.extendFunction(name, mvc.view.functions[name]);
});
Object.keys(mvc.view.filters).forEach(name => {
    twig.extendFilter(name, mvc.view.filters[name]);
});
server.set("twig options", {allow_async: true});
server.engine("twig", twig.__express);
if (config.application.dev_mode) {
    twig.cache(false);
}
--------------------------------------------------------------------------------
```

```js
--------------------------------------------------------------------------------
$("box").css("display", "none");
$("box").each(function () {
    if ($(this).html()) {
        var $bootbox = {};
        var buttons  = {};
        var type     = $(this).attr("type");
        var title    = $(this).attr("title");
        var options  = $(this).attr("options"); // options="Choice One:1, Choice Two:2, Choice Three:3"
        var locale   = {
            CONFIRM: "Confirmar",
            CANCEL: "Cancelar"
        };
        if (type === "alert") {
            $bootbox = bootbox.alert;
            buttons  = {
                ok: {
                    className: "btn-secondary"
                }
            };
        } else if (type === "confirm") {
            $bootbox = bootbox.confirm;
            buttons  = {
                cancel: {
                    label: '<i class="fa fa-times"></i> ' + locale.CANCEL,
                    className: "btn-danger"
                },
                confirm: {
                    label: '<i class="fa fa-check"></i> ' + locale.CONFIRM,
                    className: "btn-success"
                }
            };
        } else if (type === "dialog") {
            $bootbox = bootbox.dialog;
        } else {
            title = title || "Prompt: " + type;
            if (options) {
                options  = options.split(",");
                var size = options.length;
                var data = [];
                for (var i = 0; i < size; i++) {
                    data = options[i].split(":");
                    options[i] = {text: data[0], value: data[1]};
                }
            }
            $bootbox = bootbox.prompt;
            buttons  = {
                cancel: {
                    label: '<i class="fa fa-times"></i> ' + locale.CANCEL,
                    className: "btn-danger"
                },
                confirm: {
                    label: '<i class="fa fa-check"></i> ' + locale.CONFIRM,
                    className: "btn-success"
                }
            };
        }
        $bootbox({
            title: title,
            inputType: type,
            inputOptions: options,
            message: $(this).html(),
            value: ($(this).attr("value")) ? $(this).attr("value").replace(/ /g,"").split(",") : 0,
            className: $(this).attr("class"),
            multiple: ($(this).attr("multi") === "true") ? true : false,
            centerVertical: ($(this).attr("center") === "false") ? false : true,
            backdrop: ($(this).attr("backdrop") === "true") ? true : undefined,
            closeButton: ($(this).attr("close") === "false") ? false : true,
            size: $(this).attr("size"),
            buttons: buttons,
            callback: function (result) {
                if (typeof box === "function") {
                    box(result);
                }
            }
        });
    }
});
--------------------------------------------------------------------------------
```

```js
/*
| ------------------------------------------------------------------------------
| Includes Controllers and Models
| ------------------------------------------------------------------------------
*/
function include(module, layer, file) {
    var class_path = MOD_PATH + "/" + module + "/layers/" + layer,
        cache_path = CACHE_PATH + "/layers/" + layer + "/" + module,
        cache_file = cache_path + "/" + file + ".js";
    if (config.application.dev_mode === true) {
        $("file").remove(cache_file);
        if (require.cache[cache_file]) {
            delete require.cache[cache_file];
        }
    }
    if (!$("file").exists(cache_file)) {
        const terser = require("terser");
        file = $("file").read(class_path + "/" + file + ".js");
        file = file.replace(/\/\*[\s\S]*?\*\/|\/\/.*/g, "");
        var src = "",
            inc = file.match(/include\((\".*\"|\'.*\')\)(\;|)/g);
        if (inc) {
            inc.forEach(file => {
                file = file.replace(/include\(["']|['"]\)(\;|)/g, "");
                src += $("file").read(class_path + "/" + file);
            });
        }
        src += "module.exports=" + file.replace(/include\(.*\)(\;|)/g, "");
        $("directory").create(cache_path);
        $("file").create(cache_file, terser.minify(src).code);
    }
    file = require(cache_file);
    return new file;
}
--------------------------------------------------------------------------------
```

### Video download
---

```php
<?php

function download($title, $url, $format, $extension) {
    switch ($extension) {
      case 'm4a':
        $type = 'audio/m4a';
        break;
      case 'm4v':
        $type = 'video/mp4';
        break;
      case 'mp4':
        $type = 'video/mp4';
        break;
      case 'webm':
        $type = 'video/webm';
        break;
      case 'flv':
        $type = 'video/x-flv';
        break;
      case 'mov':
        $type = 'video/quicktime';
        break;
      case 'oga':
        $type = 'audio/ogg';
        break;
      case 'ogv':
        $type = 'video/ogg';
        break;
      case 'ogg':
        $type = 'application/ogg';
        break;
      case 'avi':
        $type = 'video/x-msvideo';
        break;
      case 'wav':
        $type = 'audio/x-wav';
        break;
      default:
        $type = 'video/mpeg';
    }
    header('Pragma: public');
    header('Expires: 0');
    header('Cache-Control: must-revalidate, post-check=0, pre-check=0');
    header('Cache-Control: public');
    header('Content-Description: File Transfer');
    header("Content-type: $type");
    header('Content-Disposition: attachment; filename="' .
    rawurlencode($title) . '.' . $extension . '"');
    echo readFile("https://foo.demo/download?url=$url&format=$format");
    exit;
}

?>
```

### OEmbed
---

https://noembed.com

https://github.com/leedo/noembed

https://github.com/ricardofiorani/oembed - OEmbed is a PHP library to assist you retrieving data from providers that supports OEmbed.
It was built to be a successor of ricardofiorani/php-video-url-parser

```php
<?php

function embed($url) {
    header('Content-Type: application/json; charset=utf-8');
    return file_get_contents("https://noembed.com/embed?url=$url");
}

echo embed('http://www.youtube.com/watch%3Fv%3DbDOYN-6gdRE'); // Print video data in JSON format.

?>
```

### GIT
---

leandro@sciola:~$ **git clone https://github.com/sciola-framework/sciola-framework.github.io**

leandro@sciola:~$ **git remote set-url origin https://<token>@github.com/sciola-framework/sciola-framework.github.io**

********************************************************************************

leandro@sciola:~$ **git tag -d v1.1.2**

leandro@sciola:~$ **git push --delete origin v1.1.2**

leandro@sciola:~$ **GIT_COMMITTER_DATE="2021-08-10 12:00"**

leandro@sciola:~$ **git tag -a v1.1.2 -m "v1.1.2"**

leandro@sciola:~$ **git push --tags origin main**

********************************************************************************

leandro@sciola:~$ **git status**

leandro@sciola:~$ **git add .**

leandro@sciola:~$ **git commit -m "Description..."**

leandro@sciola:~$ **git push origin main**

---

### JS - Promise

[DEMO - PROMISE](https://jsfiddle.net/dgvk612x/)

```html
<script>
function fnc(arg) {
    return new Promise(function (resolve, reject) {
        if (arg) {
            resolve(arg);
        } else {
            reject("Error");
        }
    });
}
async function demo(arg, cb) {
    return cb(await fnc(arg));
}
demo("abc", data => console.log(data));
</script>
```

---

### Compile .SCSS files

leandro@sciola:~$ **sass import.scss all.css**

leandro@sciola:~$ **sass import.scss all.min.css --style compressed**

leandro@sciola:~$ **sass import.scss all.min.css --style compressed --watch**

---

### PRISM

<https://prismjs.com>

```html
<script>
var code = "";
const prismjs = require("prismjs");
try {
    code = prismjs.tokenize(code, prismjs.languages.javascript, "javascript");
} catch(e) {
    code = prismjs.highlight(code, prismjs.languages.javascript, "javascript");
}
</script>
```
