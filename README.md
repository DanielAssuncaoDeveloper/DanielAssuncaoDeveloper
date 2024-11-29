<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=810DA9&height=120&section=header"/>
 
[![Typing SVG](https://readme-typing-svg.herokuapp.com/?color=810DA9&size=35&center=true&vCenter=true&width=1000&lines=What%27s+up%2C+I%27m+%40DanielAssuncaoDeveloper%3BI%27m+a+Backend+Developer%3BWhat%27s+up%2C+I%27m+%40DanielAssuncaoDeveloper%3BI%27m+a+Backend+Developer%21)](https://git.io/typing-svg)

<br />

<div align="center">  
  <img width="49%" height="195px" src="https://github-readme-stats-sigma-five.vercel.app/api?username=DanielAssuncaoDeveloper&show_icons=true&count_private=true&hide_border=false&title_color=810DA9&icon_color=810DA9&text_color=c9d1d9&bg_color=0d1117"%20" />
  <img width="41%" height="195px" src="https://github-readme-stats-sigma-five.vercel.app/api/top-langs/?username=DanielAssuncaoDeveloper&layout=compact&hide_border=false&title_color=810DA9&text_color=c9d1d9&bg_color=0d1117" />
</div>

<br />

<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=810DA9&height=120&section=footer"/>


                  .model small
.stack 100h

.data
    msg1 db 'Numeros antes da ordenacao: $'
    msg2 db 13, 10, 'Numeros ordenados: $'
    nums db '73914265$'  ; Números como uma string (separados por '$' no final)

.code
main:
    ; Inicializa o segmento de dados
    mov ax, @data
    mov ds, ax

    ; Exibe a mensagem de entrada
    mov ah, 09h
    lea dx, msg1
    int 21h

    ; Exibe os números antes da ordenação
    lea dx, nums
    call exibe_numeros

    ; Chama o algoritmo de ordenação (Bubble Sort)
    call bubble_sort

    ; Exibe a mensagem de saída
    mov ah, 09h
    lea dx, msg2
    int 21h

    ; Exibe os números ordenados
    lea dx, nums
    call exibe_numeros

    ; Finaliza o programa
    mov ah, 4Ch
    int 21h

; Função para exibir os números
exibe_numeros:
    lea si, nums             ; Carrega o endereço da string de números
exibe_loop:
    mov al, [si]             ; Carrega o caractere (número) da string
    cmp al, '$'              ; Verifica se é o terminador de string
    je exibe_fim
    call exibe_numero
    inc si                    ; Avança para o próximo caractere
    jmp exibe_loop
exibe_fim:
    ret

; Função para exibir um número
exibe_numero:
    mov dl, al               ; Carrega o número em dl
    mov ah, 02h
    int 21h                  ; Exibe o caractere
    ret

; Função de ordenação Bubble Sort
bubble_sort:
    lea si, nums             ; Carrega o endereço da string
    mov cx, 7                ; Número de comparações - 1 (temos 8 números - 1)
outer_loop:
    lea di, [si]             ; Inicializa o índice interno
    mov bx, cx
inner_loop:
    mov al, [di]             ; Carrega o número atual
    mov ah, [di + 1]         ; Carrega o próximo número
    cmp al, ah               ; Compara os dois números
    jbe no_swap              ; Se o número atual for menor ou igual, não troca
    ; Troca os dois números
    mov [di], ah
    mov [di + 1], al
no_swap:
    inc di                   ; Avança para o próximo caractere
    dec bx
    jnz inner_loop           ; Continua o loop interno
    dec cx
    jnz outer_loop           ; Continua o loop externo
    ret
