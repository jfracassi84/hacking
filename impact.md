## IMPACT

--//--

#### CSP

* Isso significa que mesmo que um atacante consiga injetar um código XSS no seu site, o CSP poderá indicar ao navegador para impedir a sua execução, e caso o cabeçalho não esteja devidamente configurado, o código será executado com sucesso.

--//--

#### HSTS

* A utilização de canais de comunicação sem criptografia podem acarretar em interceptação de tráfego por meio de um MiTM e consequentemente o roubo de dados, sejam formulários enviados, ou credenciais trafegadas em páginas de autenticação.

--//--

#### Clickjacking

* O ataque conhecido como clickjacking pode induzir o usuário ao engano, fazendo-o clicar em elementos invisíveis de uma página legítima. Isso o leva a realizar ações indesejadas, como por exemplo divulgar informações sem que ele perceba, executar alterações cadastrais, entre outros.

--//--

#### Brute Force

* Caso um usuário identifique uma combinação válida de usuário e senha, o atacante irá obter todos os acessos proporcionais relacionados a esta conta, podendo alterar, remover, ou adicionar dados de forma arbitrária.

--//--

#### Uso de componentes com vulnerabilidades conhecidas

* Um atacante que identificar um produto desatualizado e com múltiplas vulnerabilidades em seu alvo poderá buscar técnicas e exploits específicos para explorar o ambiente com sucesso.

--//--

#### Session Management

* O Session Storage é acessível via Javascript, tornando os tokens vulneráveis a ataques de XSS. Embora o Session Storage seja limpo ao fechar a aba, durante a sessão ativa os dados ficam expostos. Como alternativas mais seguras, usar o HttpOnly, Secure flag, manter o token com um tempo de expiração mais curto, armazenamento server-side, implementação do cabeçalho CSP, entre outros.

--//--

#### HttpOnly

* Em cenários de javascript maliciosos, pode ocorrer ataques de hijacking e exfiltração de dados como tokens ou credenciais de usuários.

--//--

#### Secure Flag

* A falta do atributo Secure em cookies de sessão permite sua transmissão por HTTP, tornando-os vulneráveis a ataques MITM e roubo de dados. Isso compromete a sessão do usuário, permitindo acesso não autorizado à conta. Sua ausência aumenta significativamente o risco de violações de segurança.
