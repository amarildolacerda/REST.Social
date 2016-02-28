# REST.Social

Delphi REST Datasnap Client Social Network
------------------------------------------

#Delphi Simplificando Datasnap com TRESTClient

O uso de Datasnap como cliente de acesso ao servidor JSON é resultante de uma combinação de componentes do delphi para completar a chamada.
Se do lado do Servidor há um Datasnap então o lado cliente é facilitado ao coletar informações dos métodos exportados pelo servidor e geração do cliente  automático.
A implementação do servidor JSON pode apresentar uma variedade muito grande de formato de publicação (ou não) dos seus métodos, o que pode se tornar bastante trabalhoso a implementação do cliente.

Simplificando o trabalho:

TRESTSocialClient
-----------------
  Encapsula os componentes necessário para efetivar uma troca de informções entre do servidor para o cliente.
<pre>  
  public
    function Response: TRESTResponse;
    function Request: TRESTRequest;
    function Auth2: TOAuth2Authenticator;
    property AccessToken: string read GetAccessToken write SetAccessToken;
    procedure Clear; virtual;
    constructor create(ow: TComponent); override;
    destructor destroy; override;
    function Get(url: string; AResource: string = ''): string; virtual;
    function GetStream(AUrl: string; AResource: string; AStream: TStream)
      : integer; virtual;
    function SendStream(AUrl, AResource: string; AStream: TStream)
      : integer; virtual;
    function Post(url: string; AResource: string = ''): string; virtual;
</pre>

  exemplo:
<pre>  
  var rsp:string;
  with TRESTSocialClient.create(nil) do
  try
    rsp := Get('http://meuservidor/xxxx', '/GetCliente?codigo=1');  // chama o servidor para pegar GetCliente....  
  
  finally
     free;
  end;
</pre>

TRESTSocialClientDataset
------------------------
  Herança de TRESTSocialClient que associa a resposta do servidor um Dataset;
<pre>  
  with TRESTSocialClientDataset.create(nil) do
  try
    // pode indica um DATASET, para obter o retorno
    Dataset := MeuDataset;   // se nao for informado retorna um Dataset   TFDMemTable
    rootElement := 'result';  // espera um Array com as linhas da tabela;  
    rsp := Get('http://meuservidor/xxxx', '/GetCliente?codigo=1');  // chama o servidor para pegar GetCliente....  
  
  finally
     free;
  end;
  </pre>
  
  


