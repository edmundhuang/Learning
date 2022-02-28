### Mono Print

1. CheckFeeder - Check if there is no card in feeder  
1.1. Card_Insert  
1.1.1 Error handling  
2. CheckRibbonEx  
2.1. Error handling  
3. CheckRibbonCount  
3.1. Error handing  
4. N_StartOfPrinting  
5. N_SetPrintType  
N_SetPrintType(0, 1, 0)

6. N_ClearImageBuffer  
7. N_SetImageBuffer  
> * int N_SetImageBuffer (int p1, int p2, int p3, int p4, int p5, int p6, char *pFile )  
> * p1[in]: X coordination(0 ~ 1013)  
> * p2[in]: Y corrdination(0 ~ 643)
> * p3[in]: ribbon setting
> ‘c’ : Color Buiffer – it saves the image to the YMC buffer.  0x63  
‘b’ : Color Buffer – it extracts the black from the image and saves to K Panle buffer.    0x62
‘k’ : Color Buffer –it saved only to K Panel buffer.  
‘m’ : Mono Buffer   0x6d
‘v’ : Varnish Buffer  
‘e’ : Mono Ext. Buffer(only for special use)
> * p4[in]: image rotation(‘0’ : 0, ‘1’ : 90, ‘2’ : 180, ‘3’ : 270)
> * p5[in]: Gray level(31, 254)   
if it is ‘v’
> * p6[in]: image processing mode
> 0x00 : none  
0x01 : sharpening(clearer)  
0x02 : diffusion filter (soft) – (diffusion –erase noise)  
0x40 : Gamma Correction (gamma correction)  

7.1. Sample
> N_SetImageBuffer(0, 0, 0x63, 0, 255, 0, "Sample1.jpg"); // last parameter = image name, image send
> p1: 0
> p2: 0
> p3: Color buffer
> p4: no rotation
> p5: no meaning
> p6: bitmap file name

8. TextToBmpMakeEx
9. N_SetImageBuffer
10. Image_VarnishSendEx
11. N_TransferImageData


### Ribbon Type
Color Ribbon / YMCKO
Mono Ribbon /  Silver