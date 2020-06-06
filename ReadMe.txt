选择的隐藏方法是LSB算法 对图片中的最低比特位进行替换 隐藏信息为57117122szy  使用工具是matlab
以下是隐藏用代码
clear all 
close all 
Img=imread('boy'.bmp'); 
Double_Img=double(Img);
fileID=fopen('test.txt','r');  
[msg,len]=fread(fileID,'ubit1');
[m,n]=size(Double_Img); 
p=1;
for f2=1:n 
for f1=1:m 
Double_Img(f1,f2)=Double_Img(f1,f2)-mod(Double_Img(f1,f2),2)+msg(p,1);
if p==len 
break;
   end p=p+1; 
end 
if p==len break; 
  end 
end 
Double_Img=uint8(Double_Img); 
imwrite(Double_Img,'result.bmp');   
subplot(121);imshow(Img);title('未嵌入信息的图片'); 
subplot(122);imshow(Double_Img);title(' 嵌入信息的图片');

以下代码代入matlab中可提取出包含“57117122szy”信息的文本文档
Img=imread('result.bpm');
Img=double(Img);
[m,n]=size(Img);
xx=fopen('result.txt','a');
len=192;
p=1;
for f2=1:n;
for f1=1:m;
if bitand (Img(f1,f2),1)==1
fwrite(xx,1,'bit');
result(p,1)=1
else
fwrite(xx,0,'bit1');
result(p,1)=0;
end
p=p+1
end
if p==len
break;
end
end
