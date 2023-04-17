tag: platech_partner

# procedimiento de como implementar FalconBot


1. Instalar Node js y npm en la computador 

- a. Ve a la página de descargas oficial de Node.js: [https://nodejs.org/en/download/](https://nodejs.org/en/download/) 

- b. Selecciona la versión "LTS" (Long Term Support) para garantizar una versión estable y con soporte a largo plazo. 

- c. Descarga el instalador para Windows (.msi). 

- d. Ejecuta el instalador y sigue las instrucciones en pantalla, dejando las opciones predeterminadas. e. Al finalizar la instalación, reinicia tu computadora.

2. realiza la instalacion de Node red

- a.  Abre una terminal (en Windows, usa la línea de comandos o PowerShell). 
- b.  Ejecuta el siguiente comando para instalar Node-RED globalmente usando npm:


para realizar dicho proceso seguir las intrucciones del siguiente video

https://www.youtube.com/watch?v=JC1nJoyemi4&ab_channel=iSebasmicroProgramando

En la ventana de node-red  importar el siguiente flow




aqui se encuentra la primera version de FalconBot

[
    {
        "id": "fd2bd8cfadf0983b",
        "type": "tab",
        "label": "Flow 1",
        "disabled": false,
        "info": "",
        "env": []
    },
    {
        "id": "5123f088baf692fb",
        "type": "group",
        "z": "fd2bd8cfadf0983b",
        "name": "check Files",
        "style": {
            "label": true
        },
        "nodes": [
            "0bcf4aef851f31fd",
            "75196e73b6d5ed1f",
            "4f4b05e822994741",
            "eea5ce7a204b68c6",
            "2acaf73b46f365bc",
            "05b4400c0eeffddb",
            "17107faffba21b44",
            "dc21109e5856f4d9",
            "a42a22b3c5aa6973"
        ],
        "x": 54,
        "y": 299,
        "w": 1042,
        "h": 202
    },
    {
        "id": "31a7d5666892a8ee",
        "type": "group",
        "z": "fd2bd8cfadf0983b",
        "name": "Convert Image and delete it",
        "style": {
            "label": true
        },
        "nodes": [
            "3acad38d7d3996a0",
            "90be7448a48f16a6",
            "0b670102e979e69b",
            "54d40125a9db2508",
            "b1227e5cc35798b1",
            "e69d54fee738b141",
            "751ccab64661ea67"
        ],
        "x": 44,
        "y": 539,
        "w": 882,
        "h": 122
    },
    {
        "id": "1c4828488a71b550",
        "type": "group",
        "z": "fd2bd8cfadf0983b",
        "name": "call falcon Motor",
        "style": {
            "label": true
        },
        "nodes": [
            "cf3d0e3b6003c633",
            "b6fa0cced77a6ce2",
            "beba21c407631436",
            "ea67774e63d2fea5"
        ],
        "x": 54,
        "y": 719,
        "w": 672,
        "h": 82
    },
    {
        "id": "3acad38d7d3996a0",
        "type": "file in",
        "z": "fd2bd8cfadf0983b",
        "g": "31a7d5666892a8ee",
        "name": "",
        "filename": "filename",
        "filenameType": "msg",
        "format": "",
        "chunk": false,
        "sendError": false,
        "encoding": "none",
        "allProps": false,
        "x": 180,
        "y": 580,
        "wires": [
            [
                "90be7448a48f16a6"
            ]
        ]
    },
    {
        "id": "90be7448a48f16a6",
        "type": "function",
        "z": "fd2bd8cfadf0983b",
        "g": "31a7d5666892a8ee",
        "name": "buffer to image 64",
        "func": "msg.payload = Buffer.from(msg.payload).toString('base64')\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 370,
        "y": 580,
        "wires": [
            [
                "b1227e5cc35798b1",
                "751ccab64661ea67"
            ]
        ]
    },
    {
        "id": "7ff04ef968375045",
        "type": "image viewer",
        "z": "fd2bd8cfadf0983b",
        "name": "",
        "width": 160,
        "data": "payload",
        "dataType": "msg",
        "active": true,
        "x": 610,
        "y": 40,
        "wires": [
            []
        ]
    },
    {
        "id": "cf3d0e3b6003c633",
        "type": "axios-request",
        "z": "fd2bd8cfadf0983b",
        "g": "1c4828488a71b550",
        "name": "FalconMotor",
        "endpoint": "1986b9880fd16d4f",
        "method": "post",
        "url": "",
        "responseType": "json",
        "keepAlive": false,
        "timeout": 30000,
        "validateStatus": true,
        "headers": [
            {
                "keyType": "str",
                "keyValue": "Content-Type",
                "valueType": "str",
                "valueValue": "application/json"
            }
        ],
        "params": [
            {
                "keyType": "str",
                "keyValue": "",
                "valueType": "str",
                "valueValue": ""
            }
        ],
        "x": 430,
        "y": 760,
        "wires": [
            [
                "ea67774e63d2fea5"
            ]
        ]
    },
    {
        "id": "b6fa0cced77a6ce2",
        "type": "link in",
        "z": "fd2bd8cfadf0983b",
        "g": "1c4828488a71b550",
        "name": "link in 1",
        "links": [
            "751ccab64661ea67"
        ],
        "x": 95,
        "y": 760,
        "wires": [
            [
                "beba21c407631436"
            ]
        ]
    },
    {
        "id": "beba21c407631436",
        "type": "function",
        "z": "fd2bd8cfadf0983b",
        "g": "1c4828488a71b550",
        "name": "create Json",
        "func": "const obj = {}\n\nobj[\"ticketType\"] = \"type1\"\nobj[\"image\"] = msg.payload\n\nmsg.payload = obj\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 210,
        "y": 760,
        "wires": [
            [
                "cf3d0e3b6003c633"
            ]
        ]
    },
    {
        "id": "0bcf4aef851f31fd",
        "type": "inject",
        "z": "fd2bd8cfadf0983b",
        "g": "5123f088baf692fb",
        "name": "path inyect",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "path",
                "v": "D:\\platech\\suserte vision ai\\final test",
                "vt": "str"
            }
        ],
        "repeat": "0.5",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "x": 170,
        "y": 420,
        "wires": [
            [
                "75196e73b6d5ed1f",
                "05b4400c0eeffddb"
            ]
        ]
    },
    {
        "id": "75196e73b6d5ed1f",
        "type": "fs-ops-dir",
        "z": "fd2bd8cfadf0983b",
        "g": "5123f088baf692fb",
        "name": "listFile",
        "path": "path",
        "pathType": "msg",
        "filter": "*",
        "filterType": "str",
        "dir": "files",
        "dirType": "msg",
        "x": 330,
        "y": 420,
        "wires": [
            [
                "4f4b05e822994741"
            ]
        ]
    },
    {
        "id": "4f4b05e822994741",
        "type": "change",
        "z": "fd2bd8cfadf0983b",
        "g": "5123f088baf692fb",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "file",
                "pt": "flow",
                "to": "files",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 470,
        "y": 420,
        "wires": [
            [
                "eea5ce7a204b68c6"
            ]
        ]
    },
    {
        "id": "eea5ce7a204b68c6",
        "type": "array-loop",
        "z": "fd2bd8cfadf0983b",
        "g": "5123f088baf692fb",
        "name": "files",
        "key": "aleea5ce7a204b68c6",
        "keyType": "msg",
        "reset": false,
        "resetValue": "value-null",
        "array": "file",
        "arrayType": "flow",
        "x": 630,
        "y": 420,
        "wires": [
            [],
            [
                "2acaf73b46f365bc"
            ]
        ]
    },
    {
        "id": "2acaf73b46f365bc",
        "type": "delay",
        "z": "fd2bd8cfadf0983b",
        "g": "5123f088baf692fb",
        "name": "",
        "pauseType": "delay",
        "timeout": "0.25",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "allowrate": false,
        "outputs": 1,
        "x": 770,
        "y": 420,
        "wires": [
            [
                "17107faffba21b44"
            ]
        ]
    },
    {
        "id": "05b4400c0eeffddb",
        "type": "change",
        "z": "fd2bd8cfadf0983b",
        "g": "5123f088baf692fb",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "path",
                "pt": "flow",
                "to": "path",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 330,
        "y": 340,
        "wires": [
            []
        ]
    },
    {
        "id": "17107faffba21b44",
        "type": "function",
        "z": "fd2bd8cfadf0983b",
        "g": "5123f088baf692fb",
        "name": "inyect Path",
        "func": "msg.filename = `${flow.get('path')}\\\\${msg.payload}`\nflow.set(\"filename\", msg.filename)\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 930,
        "y": 420,
        "wires": [
            [
                "dc21109e5856f4d9"
            ]
        ]
    },
    {
        "id": "dc21109e5856f4d9",
        "type": "link out",
        "z": "fd2bd8cfadf0983b",
        "g": "5123f088baf692fb",
        "name": "link out 2",
        "mode": "link",
        "links": [
            "0b670102e979e69b"
        ],
        "x": 1055,
        "y": 420,
        "wires": []
    },
    {
        "id": "0b670102e979e69b",
        "type": "link in",
        "z": "fd2bd8cfadf0983b",
        "g": "31a7d5666892a8ee",
        "name": "link in 2",
        "links": [
            "dc21109e5856f4d9"
        ],
        "x": 85,
        "y": 580,
        "wires": [
            [
                "3acad38d7d3996a0"
            ]
        ]
    },
    {
        "id": "54d40125a9db2508",
        "type": "fs-ops-delete",
        "z": "fd2bd8cfadf0983b",
        "g": "31a7d5666892a8ee",
        "name": "",
        "path": "",
        "pathType": "str",
        "filename": "filename",
        "filenameType": "msg",
        "x": 770,
        "y": 580,
        "wires": [
            [
                "e69d54fee738b141"
            ]
        ]
    },
    {
        "id": "b1227e5cc35798b1",
        "type": "change",
        "z": "fd2bd8cfadf0983b",
        "g": "31a7d5666892a8ee",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "filename",
                "pt": "msg",
                "to": "filename",
                "tot": "flow"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 590,
        "y": 580,
        "wires": [
            [
                "54d40125a9db2508"
            ]
        ]
    },
    {
        "id": "e69d54fee738b141",
        "type": "link out",
        "z": "fd2bd8cfadf0983b",
        "g": "31a7d5666892a8ee",
        "name": "link out 3",
        "mode": "link",
        "links": [
            "a42a22b3c5aa6973"
        ],
        "x": 885,
        "y": 580,
        "wires": []
    },
    {
        "id": "a42a22b3c5aa6973",
        "type": "link in",
        "z": "fd2bd8cfadf0983b",
        "g": "5123f088baf692fb",
        "name": "link in 3",
        "links": [
            "e69d54fee738b141"
        ],
        "x": 545,
        "y": 460,
        "wires": [
            [
                "eea5ce7a204b68c6"
            ]
        ]
    },
    {
        "id": "751ccab64661ea67",
        "type": "link out",
        "z": "fd2bd8cfadf0983b",
        "g": "31a7d5666892a8ee",
        "name": "link out 4",
        "mode": "link",
        "links": [
            "b48a794572c2d741",
            "b6fa0cced77a6ce2"
        ],
        "x": 525,
        "y": 620,
        "wires": []
    },
    {
        "id": "b48a794572c2d741",
        "type": "link in",
        "z": "fd2bd8cfadf0983b",
        "name": "link in 4",
        "links": [
            "751ccab64661ea67"
        ],
        "x": 505,
        "y": 40,
        "wires": [
            [
                "7ff04ef968375045"
            ]
        ]
    },
    {
        "id": "ea67774e63d2fea5",
        "type": "debug",
        "z": "fd2bd8cfadf0983b",
        "g": "1c4828488a71b550",
        "name": "debug 4",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "statusVal": "",
        "statusType": "auto",
        "x": 620,
        "y": 760,
        "wires": []
    },
    {
        "id": "1986b9880fd16d4f",
        "type": "axios-endpoint",
        "name": "",
        "baseURL": "http://54.208.91.82:4000",
        "caCertPath": "",
        "rejectUnauthorized": true,
        "proxyEnabled": false,
        "proxyProtocol": "https",
        "proxyHost": "",
        "proxyPort": ""
    }
]





# certificados autofirmados

nos encontramos utilizado certificados autofirmados por lo que el navegador lo reconoce como no seguro ya es agregar los certificados a traefick con los tengamos
