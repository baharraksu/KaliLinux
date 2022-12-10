#!/bin/bash
echo "Projenin 1.Argümanı :$1";
echo "Prjenin 2.Argümanı :$2";
satirSayisi=$(wc -l < $1 ); #1.argümanın satır sayısını bulduk
dosyaAdi=$1
uzantisizDosyaAdi=$(echo "$dosyaAdi"|cut -d '.' -f 1);  #cut ile delimeterı . olan yerden öncesini aldım
dosyaUzantisi=`echo "$dosyaAdi"|cut -d '.' -f 2`;
#dosyaUzantisiz="${dosyaAdi%%.*}"
#dosyaUzantili="${dosyaAdi%.*}"
#variable=cut -d ' ' -f 1 | wc -l $1
echo "$uzantisizDosyaAdi"
echo "$dosyaUzantisi"
dosyaSatir=$(($satirSayisi/$2))
Nokta=".";
if [ $# -ne 2 ] #Girilen argümanlar 2 tane olmalıdır.
then
	echo "Hata: 2 tane argüman girmeniz gerekiyor";
elif [[ $2 -lt 0 ]]  #2. argüman 0 dan büyük olmalıdır.
then
	echo "Hata: Girilen 2. argüman 0 dan büyük olmalıdır.";
#elif [[ grep (\.\d*)?) ]]
elif [[ -z  "${2##*[!0-9]*}" ]]; #Tam sayı kontrolü 
then
	echo "Hata: Tam sayı giriniz";
elif [ -d $1 ]   #Dosya mıdır kontrolü
then
	echo "Geçerli dosya giriniz.";
elif (( $satirSayisi < $2 ))  #2. argüman 1  argümandan büyük olamaz.
then
	echo "Hata: Girdiğiniz argüman 1. argümandan daha büyüktür";
else
dosyaSayaci=1
sayac=0
	while read line
	do
		for((j=1;j<=$dosyaSatir;j++))
		do
			((sayac++))
			for((k=1;k<=$2;k++))
			do
			#	cat >> $uzantisizDosyaAdi$k$Nokta$dosyaUzantisi
				if(($sayac>=$2))
				then
					((dosyaSayaci++))
					sayac=1 				fi
				echo $line >> $uzantisizDosyaAdi-$dosyaSayaci$Nokta$dosyaUzantisi
				break
			done
			break
		done
	done<$1
fi

