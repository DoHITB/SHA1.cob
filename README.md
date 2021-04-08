# SHA1.cbl
Secure Hash Algorithm - 1 (SHA1) COBOL Implementation.       
                                                             
This code was written by David O. Solé González (aka DoHITB).
                                                             
The implementation was made following rfc3174 official text. You can find the mentioned rfc on the Internet for free, on http://www.ietf.org/rfc/rfc3174.txt

For any comment, suggestion or similar, you can reach me via mail on "doscar.sole@gmail.com"                              


## Important notice
We moved to new repository: https://github.com/DoHITB/CryptoCobol


## General lines and commentaries:   
- This programs only works on ASCII data passed as X(n). 
                                                             
- Once the input arrived, its transofmed into bytes.     
                                                             
- Then, the data is padded to 16 32-bit word, following the rfc algorithm:                                     
  * Add 1 on position n + 1 where n is the length of the original string.                             
                                                             
  * Fill with 0's until #14 word.                    
                                                             
  * Words #15 and #16 are for putting the HEX value of the original length. In our case, as the original input is limited to 256, #15 word will be always 0's, and also the first half of #16.   
                                                             
- After padding, the data is being amplied to 80 32-bytes words. Each word from #17 to #80 is filled according to the rfc:                                               
  * W(t) = S^1(W(t-3) XOR W(t-8)                     
           XOR W(t-14) XOR W(t-16))                  
                                                             
- Finally, the output is calculated, according to rfc:   
  * TEMP = S^5(A) + f(t;B,C,D) + E + W(t) + K(t);    
    E = D;  D = C;  C = S^30(B);  B = A; A = TEMP;   
                                                             
- After all this process, we rearrange the H's data:     
  * H0 = H0 + A                                      
  * H1 = H1 + B                                      
  * H2 = H2 + C                                      
  * H3 = H3 + D                                      
  * H4 = H4 + E                                      
                                                             
- The concatenation of all H's is the message digest.    
