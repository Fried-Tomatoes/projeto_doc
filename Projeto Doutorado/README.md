Projeto LaTeX - estrutura básica

## Arquivos criados:
- main.tex: arquivo principal que inclui as seções em `sections/`
- sections/0_pre_textuais.tex: capa, resumo, agradecimentos, sumário
- sections/1_introducao.tex: introdução
- sections/2_objetivos.tex: objetivos
- sections/3_metodologia.tex: metodologia

## ✨ Novo: Quebra Automática de Equações Longas

O projeto agora está configurado com o pacote **breqn** que permite quebra automática de equações longas.

### Como usar:
- Para equações **curtas**: use `\begin{equation}...\end{equation}` normalmente
- Para equações **longas**: use `\begin{dmath}...\end{dmath}` para quebra automática

### Documentação:
- Veja `EQUACOES_LONGAS.md` para guia completo de uso
- Veja `exemplo_uso_breqn.tex` para exemplos práticos

### Exemplo rápido:
```latex
% Equação longa com quebra automática
\begin{dmath}
\gamma(T,P) = \frac{1}{2A} \left[ G_{\text{slab}}(T,P,N_{\text{M}},N_{\text{W}},N_{\text{O}}) - N_{\text{M}}\mu_{\text{M}}(T,P) - N_{\text{W}}[g^{bulk}_{M_xWO_4}(T,P) - x\mu_{M}(T,P) - 4\mu_{O}(T,P)] - N_{\text{O}}\mu_{\text{O}}(T,P) \right]
\label{eq:exemplo}
\end{dmath}
```

## Como compilar (PowerShell, Windows):

```powershell
cd "d:\OneDrive\UNICAMP\Doutorado\Projeto\4 - Qualificação\Qualificação Geral\latex-project"
pdflatex -interaction=nonstopmode -synctex=1 main.tex
pdflatex -interaction=nonstopmode -synctex=1 main.tex
```

Observações:
- Os nomes dos arquivos foram normalizados para evitar problemas com acentuação em caminhos (ex: `1_introducao.tex`). Se preferir, posso renomeá-los para usar acentos exatamente como escreveu.
- Recomendo usar TeX Live ou MiKTeX instalados. Para compilação automática com dependências (bibliografia), use `latexmk -pdf main.tex`.

Para compilar com a bibliografia (usar biber):

```powershell
cd "d:\OneDrive\UNICAMP\Doutorado\Projeto\4 - Qualificação\Qualificação Geral\latex-project"
pdflatex -interaction=nonstopmode -synctex=1 main.tex
biber main
pdflatex -interaction=nonstopmode -synctex=1 main.tex
pdflatex -interaction=nonstopmode -synctex=1 main.tex
```

Notas sobre o estilo de referências:
- O projeto usa `biblatex` com `style=numeric`, que gera citações numéricas entre colchetes `[1]` — isso atende ao pedido de numeração com colchetes.
- Se você precisar do formato ABNT estrito (ordem dos elementos, pontos, maiúsculas etc.), posso migrar para o pacote `biblatex-abnt` (recomendado) ou para um estilo BibTeX ABNT (`abnt-num.bst`) dependendo do que estiver instalado na sua distribuição TeX.

Problema: latexmk reclama que o Perl não está instalado
---------------------------------------------------

Se você recebeu um erro semelhante a:

```
MiKTeX could not find the script engine 'perl' which is required to execute 'latexmk'.
```

Então o `latexmk` (que é um script Perl) não consegue ser executado porque o `perl` não está disponível no seu PATH.

Opções para resolver:

- Instalar o Perl (recomendado):
	- Baixe e instale o Strawberry Perl (recomendado no Windows): https://strawberryperl.com/
	- Após a instalação, abra um novo PowerShell e verifique com:

```powershell
perl -v
```

	- Depois disso, o `latexmk` deve funcionar novamente.

- Alternativa sem instalar Perl:
	- Use os comandos diretos (pdflatex + biber) — criei um script PowerShell `build.ps1` no mesmo diretório que executa a sequência necessária.
	- Para usar o script, execute no PowerShell a partir da pasta do projeto:

```powershell
cd "d:\OneDrive\UNICAMP\Doutorado\Projeto\4 - Qualificação\Qualificação Geral\latex-project"
.\build.ps1
```

	- O `build.ps1` verifica se `pdflatex` e `biber` estão disponíveis e executa a sequência de compilação (pdflatex → biber → pdflatex → pdflatex).

Se quiser, posso também:
- ajudar a instalar o Strawberry Perl passo a passo,
- ajustar o `build.ps1` para suportar compilações incrementais ou limpar artefatos, ou
- configurar um atalho no VS Code para executar o script automaticamente.
