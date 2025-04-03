+++
title = "Corrigir Cedilha (ç) Exibido como Ć no Ubuntu com Teclado US International"
date = "2025-04-02"
draft = false
+++

## Problema

No Ubuntu, ao usar um layout de teclado como "English (US, intl., with dead keys)", digitar a cedilha (`' + c`) pode resultar em `ć` em vez de `ç` em aplicativos como Slack, Skype e Firefox, mesmo com o idioma pt-BR configurado.

## Solução Principal (GTK 2/3 e Qt)

1.  **Edite o arquivo `/etc/environment` como root:**
    ```bash
    sudo gnome-text-editor /etc/environment
    ```

2.  **Adicione as seguintes linhas ao final do arquivo:**
    ```
    GTK_IM_MODULE=cedilla
    QT_IM_MODULE=cedilla
    ```

3.  **Salve o arquivo e feche o editor.** 

4.  **Reinicie a sessão ou o computador:** Faça logout e login novamente, ou reinicie o sistema para aplicar a alteração.

## Solução Adicional para Aplicativos GTK 4

Aplicativos mais recentes (como o editor de texto padrão do Ubuntu 24.04) podem exigir passos adicionais:

1.  **Crie o arquivo `~/.XCompose`** (no seu diretório pessoal) com o seguinte conteúdo:
    ```
    # UTF-8 (Unicode) compose sequences

    # Overrides C acute with Ccedilla:
    <dead_acute> <C> : "Ç" Ccedilla
    <dead_acute> <c> : "ç" ccedilla
    ```

2.  **Execute o comando no terminal:**
    ```bash
    gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/IMModule':<'ibus'>}"
    ```

3.  **Reinicie a sessão ou o computador.**


## Solução Manual (Alternativa)

Se as soluções acima não funcionarem ou não puderem ser aplicadas, use os seguintes atalhos com layouts "English (Intl)":

*   `ç`: Pressione `AltGr` + `,` (vírgula)
*   `Ç`: Pressione `AltGr` + `Shift` + `,` (vírgula)


## Referências:

* [Ajeitando Cedilha Errado no Ubuntu Linux](https://www.danielkossmann.com/pt/ajeitando-cedilha-errado-ubuntu-linux/)
* [Enabling Cedilla (Acute C) on GNOME](https://garajau.com.br/2021/02/enabling-cedilla-acute-c-on-gnome)