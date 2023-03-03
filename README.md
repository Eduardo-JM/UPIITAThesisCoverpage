# Formato estándar para portadas de tesis de la UPIITA

## Explicación de la estructura

Se tienen varias carpetas para mejorar la legibilidad del documento LaTeX.

```bash
├── Bib
│   ├── Acronyms.tex
│   ├── Glossary.tex
│   └── References.bib
├── Diagrams
├── Figures
│   └── logos
│       ├── IPN.png
│       └── UPIITA.png
├── main.tex
├── Preamble
│   ├── ComplexCommands.tex
│   ├── Config.tex
│   ├── Coverpage.tex
│   ├── CustomKeys.tex
│   ├── Packages.tex
│   └── Preamble.tex
├── Readme.md
├── Tcolorbox
└── Tikz
```

El archivo principal es `main.tex`, deberás gestionar todo tu documento desde ahí.

Se inicia importando `Preamble/Preamble.tex`, archivo donde se gestiona todos los paquetes utilizados, la configuración, comandos y llaves definidas por el usuario. Me tomé la libertad de colocar en este archivo las librerías que más uso y algunas mejoras al rendimiento como la **externalización** en `Tikz` y en `tcolorbox`.

Si apenas comienzan con LaTeX o no usan muchas figuras de `pgf`, pueden eliminar todo lo que diga "external" para evitarse complicaciones, aunque es sugerido conocerlo y aplicarlo.

## ¡Importante!

1. Se recomienda compilar el código LaTeX con `XeLaTeX` aunque `LuaLaTeX` también sería una alternativa.

2. Para las referencias está siendo considerado el uso de  `Biber` , te sugeriría usarlo también, pero si no, recuerda modificarlo en `Preambles/Packages.tex`

3. Mi sistema operativo no tenía instaladas las fuentes que piden para la Portada, por lo que se agregaron manualmente en  `Preambles/Config.tex`.

   ```LaTeX
   % Define a new Font family, use only if it doesn't recognize your fonts
   
   \newfontfamily{\BellMT}{Bell MT}[
   	Extension = .ttf,
   	Path = /usr/share/fonts/bell-mt/,
   	BoldFont = BELLB,
   	ItalicFont = BELLI
   ]
   
   \newfontfamily{\Footlight}{FTLTLT}[
   	Extension = .ttf,
   	Path = /usr/share/fonts/Footlight-MT/,
   	BoldFont = footlight-mt-bold
   ]
   ```

   Por lo que se pide checar esta parte antes de ejecutar.

4. Si trabajas desde escritorio como es mi caso, te recomiendo este script de ejecución

   ```
   xelatex -synctex=1 -interaction=nonstopmode --output-directory=./build --shell-escape %.tex
   makeindex -t %.glg -s %.ist -o %.gls %.glo
   makeindex -t %.alg -s %.ist -o %.acr %.acn
   biber --output-directory=./build %
   ```

   Donde `%` es el nombre del archivo sin extensión

## ¿Qué sigue?
Por mi parte estaré subiendo en un futuro próximo la siguiente hoja de firmas de la tesis. Si encuentran algún error o forma de optimizar el proceso avisarme de favor para corregirlo/implementar en la brevedad.