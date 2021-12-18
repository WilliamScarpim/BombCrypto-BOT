

# Sobre

Este repositório é um fork do https://github.com/mpcabete/bombcrypto-bot, com as minhas modificações.

Bot para realizar cliques automaticos no jogo BombCrypto, com reconhecimento de telas e botões, podendo ficar longe do computador enquanto o Python joga sozinho.
- Resolução automatica de captcha.
- Integração com Telegram, enviando status, quantidade de BCoins e print dos mapas.


### Aviso:

Os desenvolvedores do jogo Bombcrypto se pronunciaram e agora o uso de auto clickers e o uso de bots é oficialmente PROIBIDO.
Não me responsabilizo por eventuais penalidades sofridas por quem usar o bot, use por sua própria conta e risco.



# Instalação (windows):

Baixe e instale o Python pelo [site](https://www.python.org/downloads/) ou pela [windows store](https://www.microsoft.com/p/python-37/9nj46sx7x90p?activetab=pivot:overviewtab).

Se você baixar pelo site é importante marcar a opção para adicionar o
python ao PATH:
![Check Add python to PATH](https://github.com/mpcabete/bombcrypto-bot/raw/ee1b3890e67bc30e372359db9ae3feebc9c928d8/readme-images/path.png)

### Realize o download do codigo no formato zip, e extraia o arquivo.

### Copie o caminho até a pasta do bot:

![caminho](https://github.com/mpcabete/bombcrypto-bot/raw/main/readme-images/address.png)

### Abra o terminal.

Aperte a tecla do windows + r e digite "cmd":

![launch terminal](https://github.com/mpcabete/bombcrypto-bot/raw/main/readme-images/cmd.png)

### Navegue até a pasta do bot:
Digite o comando "cd" + caminho que você copiou:

![cd](https://github.com/mpcabete/bombcrypto-bot/raw/main/readme-images/cd.png)

### Instale as dependências:

```
pip install -r requirements.txt
```

  
![pip](https://github.com/mpcabete/bombcrypto-bot/raw/main/readme-images/pip.png)



### Edite os dados do Telegram

Faça uma cóia do arquivo `config.yaml.example` e renomeie para `config.yaml`. Após isso, no arquivo `config.yaml`, insira seus dados do Telegram, caso queira utilizar essa opção. Caso contrario, deixe como está. 


1. Go to official telegram BotFather (https://t.me/BotFather/)

2. Create your bot and copy bot-token (eg. 5021546203:AAHeK199jW25dfvslkOhMzAumzVecSxvVZw )

3. Open config.yaml in your bot folder and paste bot-token to "telegram_token"

4. In config.yaml set "log_telegram" to "True"

5. Go to userinfobot (https://t.me/userinfobot) , send "/start" and copy your telegram id

6. In config.yaml set "telegram_chat_id" to your telegram_id

7. Go to your telegram bot and send "/start"

8. Start bot



### Pronto! Agora é só iniciar o bot com o comando

```
python index.py
```

![run](https://github.com/mpcabete/bombcrypto-bot/raw/main/readme-images/run.png)


# Como usar?

Abra o terminal, se ainda não tiver navegado para a pasta do bot dê novamente o comando

```
"cd" + caminho que você copiou
```

Para iniciar use o comando 

```
python index.py
```

Assim que ele iniciar ele vai começar mandando os bonecos trabalhar. Para que ele funcione é preciso que a janela do game esteja aparecendo na sua tela.
Ele vai constantemente checar se você foi desconectado para realizar o login novamente, e se o botão “new map” tá na tela para clicar nele.
A cada 15 minutos ele manda todos os heróis taralharem.


## Como funciona?

O bot não interage diretamente com o jogo, ele somente tira print da tela do
game para encontrar os botões e simula movimentos do mouse, isso faz com que
diferenciar o bot de um humano seja muito difícil.

## Ajustando o bot

### Por que uns ajustes podem ser necessários?

O bot usa reconhecimento de imagem para tomar decisões e movimentar o mouse e
clicar nos lugares certos. 
Ele realiza isso comparando uma imagem de exemplo com um screenshot da tela do
computador.
Este método está sujeito a inconsistências devido a diferenças na resolução da
sua tela e de como o jogo é renderizado no seu computador comparado com o
meu(o que usei para pegar as imagens exemplo).
É provável que o bot não funcione 100% logo de cara, e que você precise fazer
alguns ajustes aqui ou ali.

### Quais sao os problemas?

**Falso negativo** - O bot deveria reconhecer uma imagem, por exemplo, o botão de
mandar para trabalhar, mas não reconheceu a imagem na screenshot.

**Falso positivo** - O bot pensa que reconheceu a imagem que está procurando em um
lugar em que esta imagem não aparece.

Aqui tem uma [lista](#alguns-comportamentos-que-podem-indicar-um-falso-positivo-ou-negativo) de alguns problemas que podem ser ocasionados por falsos
positivos e negativos.

Para resolver estes problemas existem duas possibilidades, a regulagem do
parâmetro “threshold” no arquivo config.yaml ou a substituição da imagem de
exemplo na pasta “targets” para uma tirada no seu próprio computador:

  ### Threshold na config

  O parâmetro “threshold” regula o quanto o bot precisa estar confiante para
  considerar que encontrou a imagem que está procurando.
  Este valor de 0 a 1 (0% a 100%).
  Ex:

  Um threshold de 0.1 é muito baixo, ele vai considerar que encontrou a imagem
  que esta procurando em lugares que ela não está aparecendo ( falso positivo ).
  O comportamento mais comum pra esse problema é o bot clicando em lugares
  aleatórios pela tela. 


  Um threshold de 0.99 ou 1 é muito alto, ele não vai encontrar a imagem que
  está procurando, mesmo quando ela estiver aparecendo na tela. O comportamento
  mais comum é ele simplesmente não mover o cursor para lugar nenhum, ou travar
  no meio de um processo, como o de login.

  ### Substituição da imagem na pasta targets

  As imagens exemplo são armazenadas na pasta “targets”. Estas imagens foram
  tiradas no meu computador e podem estar um pouco diferente da que aparece no
  seu. Para substituir alguma imagem que não esta sendo reconhecida
  propriamente, simplesmente encontre a imagem correspondente na pasta targets,
  tire um screenshot da mesma área e substitua a imagem anterior. É importante
  que a substituta tenha o mesmo nome, incluindo o .png.

### Alguns comportamentos que podem indicar um falso positivo ou negativo

#### Falso positivo:

- Repetidamente enviando um herói que já esta trabalhando para trabalhar em um
  loop infinito.
  - Falso positivo na imagem “go-work.png”, o bot acha que esta vendo o botão
    escuro em um herói com o botão claro.

- Clicando em lugares aleatórios(geralmente brancos) na tela
  - Falso positivo na imagem sign-button.png

 
 #### Falso negativo:

- Não fazendo nada
	- Talvez o bot esteja tendo problemas com a sua resolução e não esta
    reconhecendo nenhuma das imagens, tente mudar a configuração do navegador
    para 100%.

- Não enviando os heróis para trabalhar
	- Pode ser um falso negativo na imagem green-bar.png caso a opção
    “select_heroes_mode” estiver como “green”.


### Algumas configuraçoes podem ser mudadas no arquivo config.yaml, nao se esqueça de reiniciar o bot caso mude as configuraçoes.
