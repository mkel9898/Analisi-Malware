; Salva il valore attuale del registro base (ebp) nello stack
push    ebp
; Inizializza il registro di base (ebp) con il valore corrente dello stack
mov     ebp, esp
; Salva il registro ecx nello stack
push    ecx
; Prepara il valore 0 nello stack come dwReserved
push    0               ; dwReserved
; Prepara il valore 0 nello stack come lpdwFlags
push    0               ; lpdwFlags
; Chiama la funzione InternetGetConnectedState
call    ds:InternetGetConnectedState
; Salva il valore di ritorno della funzione in [ebp+var_4]
mov     [ebp+var_4], eax
; Confronta il valore salvato con 0
cmp     [ebp+var_4], 0
; Se il valore è zero, salta a loc_40102B
jz      short loc_40102B

; Mette l'offset di aSuccessInterne (presumibilmente un puntatore a una stringa di successo) nello stack
push    offset aSuccessInterne
; Chiama la funzione sub_40117F (probabilmente per gestire l'output o il log del successo)
call    sub_40117F
; Dopo la chiamata, libera lo spazio allocato per gli argomenti dalla pila (4 byte)
add     esp, 4
; Imposta il registro eax a 1 (probabilmente per indicare un successo)
mov     eax, 1
; Salta a loc_40103A (probabilmente per continuare l'esecuzione del programma)
jmp     short loc_40103A

; Etichetta che indica il punto di destinazione nel caso in cui manchi una connessione Internet
loc_40102B:
; Mette l'offset di aError1_1NoInte (probabilmente un puntatore a una stringa di errore) nello stack
push    offset aError1_1NoInte
; Chiama la funzione sub_40117F (probabilmente per gestire l'output o il log dell'errore)
call    sub_40117F
; Dopo la chiamata, libera lo spazio allocato per gli argomenti dalla pila (4 byte)
add     esp, 4
; Imposta il registro eax a 0 (probabilmente per indicare un errore)
xor     eax, eax

; Etichetta che indica il punto di destinazione dopo il salto
loc_40103A:
; Ripristina il registro stack pointer (esp) al valore precedente al cambio di contesto
mov     esp, ebp
; Ripristina il valore del registro di base (ebp) dallo stack
pop     ebp
; Restituisce il controllo alla funzione chiamante
retn
; Fine della procedura sub_401000
sub_401000 endp
