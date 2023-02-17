<!DOCTYPE html>
<html>
  <head>
  <body>
  <h1>Pentaho Data Integration para geração de Password Digest e TimeStamp para SOAP-WS Security</h1>
  <br>
  <br>
    <h1>Visão Geral</h1>
    <p>Este custom-step foi criado para gerar Password Digests e TimeStamps em conformidade com o padrão da OASIS Web Services Security Username Token Profile Version 1.1.1. Ele foi desenvolvido para ser usado em requisições SOAP e pode ser facilmente integrado em fluxos de transformação do Pentaho.</p>
    <h2>Detalhes Técnicos</h2>
    <h3>UsernameToken</h3>
    <p>A lógica para geração do Password Digest foi implementada no step Java Class, na função pública: <br><br><code>public boolean processRow(StepMetaInterface smi, StepDataInterface sdi) throws KettleException{}</code>.<br><br> A função foi construída utilizando Java e segue as especificações da OASIS. O Password Digest é gerado a partir do algoritmo SHA-1, que cria um hash da concatenação dos valores de Nonce, Created e Password. Em seguida, o hash é codificado em Base64.</p>
    <br>
    <code> Password_Digest = Base64 ( SHA-1 ( nonce + created + password ) ) </code>
     <br>
     <br>
    <p>Os seguintes campos é retornado para utilização e geração do Password Digest:</p>
    <ul>
      <li>Password: Senha utilizada na geração do Password Digest.</li>
      <li>Nonce: Valor aleatório utilizado na geração do Password Digest.</li>
      <li>Created: Data e hora de criação do Password Digest, no formato "yyyy-MM-dd'T'HH:mm:ss'Z'".</li>
      <li>Password Digest: Resultado da geração do Password Digest.</li>
      <li>TokenID: Valor aleatório para a tag pai &lt;wsse:UsernameToken wsu:Id=””&gt;.</li>
    </ul>
    <h3>TimeStamp</h3>
    <p>Este custom-step também permite gerar TimeStamps para requisições SOAP. Que retorna os seguintes campos:</p>
    <ul>
      <li>Created: Data e hora de criação do TimeStamp, no formato "yyyy-MM-dd'T'HH:mm:ss'Z'".</li>
      <li>Expires: Data e hora de criação acrescido de um minuto para expiração.</li>
    </ul>
    <h2>Utilização</h2>
    <p>Para utilizar este custom-step, basta adicioná-lo ao fluxo de transformação do Pentaho e configurar o ÚNICO campo de entrada "PASSWORD". O resultado da geração do Password Digest será armazenado no campo "digest".</p>
    <h2>Dificuldades Encontradas</h2>
    <p>Durante o desenvolvimento deste custom-step, enfrentei dificuldades em encontrar informações sobre a integração do Pentaho com SOAP. No entanto, após pesquisa aprofundada e testes, consegui criar este gerador de Password Digest e TimeStamp em conformidade com as especificações da OASIS.</p>
    <h2>Conclusão</h2>
    <p>Com este custom-step, é possível gerar Password Digests e TimeStamps para requisições SOAP de forma rápida e fácil, seguindo as especificações da OASIS Web Services Security Username Token Profile Version 1.1.1. A implementação foi realizada no step Java Class, que é reconhecido pelo PDI no fluxo de steps, permitindo uma integração flexível e personalizada.<p>
