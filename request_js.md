### REQUISÇÕES VIA JAVASCRIPT

#### Interceptador de requisições fetch para um servidor Web

<p>O código é um interceptor de requisições fetch, projetado para monitorar e registrar detalhes das requisições HTTP (como método, URL e cabeçalhos) feitas pela página. Ele armazena logs em window.requestLogs (embora o código atual não adicione nada a esse array) e pode ser usado para depuração, análise de tráfego de rede ou auditoria de requisições.</p>

```javascript
(function() {
    console.log("Interceptor ativado. Capturando requisições...");

    window.requestLogs = [];

    const originalFetch = window.fetch;
    window.fetch = function(resource, config) {
        const method = (config && config.method) || 'GET';
        const url = resource instanceof Request ? resource.url : String(resource);
        const headers = (config && config.headers) || {};

        console.log(`[FETCH] ${method} ${url}`);
        window.requestLogs.push({ method, url, headers });

        return originalFetch(resource, config);
    };
})();
```


#### Requisição HTTP assincrona para um servidor web

<p>O código cria um Web Worker que faz uma requisição HTTP a um endpoint específico, processa a resposta como texto e a envia de volta ao thread principal, onde é exibida no console. Ele é útil para realizar operações de rede sem impactar a performance da página.</p>

```javascript
const workerCode = `
    fetch('https://185.252.235.173:4444/data')
        .then(r => r.text())
        .then(t => postMessage(t))
        .catch(err => postMessage('Erro: ' + err.message));
`;

const blob = new Blob([workerCode], { type: 'application/javascript' });
const worker = new Worker(URL.createObjectURL(blob));

worker.onmessage = function(e) {
    console.log("Resposta:", e.data);
    worker.terminate(); // Finaliza o Worker após receber a resposta
};
```


### Requisição HTTP usando API fetch do Javascript

<p>O código faz uma requisição HTTP GET para https://185.252.235.173:4444/data, converte a resposta em texto e exibe esse texto no console. Se ocorrer algum erro (como falha na conexão ou resposta inválida), o erro é exibido no console.</p>

```javascript
fetch('https://185.252.235.173:4444/data')
    .then(res => res.text())
    .then(text => console.log(text))
    .catch(err => console.error(err));
```