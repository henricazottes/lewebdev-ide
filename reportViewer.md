<!-- @import "index.js" -->
# Test
```javascript {cmd="node" hide id="global"}
const { exec } = require('child_process');

execTestExoOne = () => exec(`npm test -- -t "Exo 1"`, (error, stdout, stderr) => {
        const json_s = stdout.split('\n').find(line => line.startsWith("{"))
        const json = JSON.parse(json_s)
        const { testResults } = json;
        const { startTime, endTime, assertionResults } = testResults[0];
        const { title, status } = assertionResults[0];
        const duration = (endTime - startTime)/1000;
        const duration_s = `${duration.toPrecision(2)}s`
        const status_s = (status == "failed" ? `✘ ` : `✔ `) +  status;
        // console.log("Duration:", duration_s);
        // console.log(JSON.stringify(json, null, 2))
        // const json = JSON.parse(stdout);
        // console.log("Json:", json)

        // console.log('stderr: ' + stderr);
        // if (error !== null) {
        // //      console.log('exec error: ' + error);
        // }
        console.log(`
        <table style="width: 100%; display: table;">
        <tbdoy>
                <tr>
                        <td>${title}</td>
                        <td>${duration_s}</td>
                        <td>${status_s}</td>
                </tr>
        </tbody>
        </table>
        `);
});

Object.defineProperty(global, 'TestExoOne', { get: execTestExoOne });
```

``` javascript {cmd="node TestExoOne" continue="global" output="html"}
TestExoOne
```

``` javascript {cmd="node" hide}
const toto = "Titi";
console.log(toto);
```