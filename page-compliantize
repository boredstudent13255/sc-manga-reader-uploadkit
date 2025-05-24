cd "$(dirname "$0")"
cd zzChapterPagesInput/
mkdir tmp

#Get information for filling out the final output filename
echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; echo " "; 

echo "You will be asked for the following: 'Series ID', 'Chapter Number'."
echo "These go as follows in filenames: '[Series ID] - [Chapter Number] -p01.jpg'"
echo " "
read -p "Please enter series ID, ex 'wataoshi', 'chou-kuse' " seriesid
read -p "Please enter [chapter string] / [2+ digit chapter number] " chaptnum

read -p "Is '$seriesid-c$chaptnum-p01.jpg' correct? [Y/n] " dohalt
if [ "$dohalt" == "n" ];
then
  exit 1
fi


####First page run to gather info while gathering info on how to handle the remaining pages

#filename="image_0$((56)).jpg"
filename=$(ls | head -1)
echo "Working on "$filename

originalfilename=$filename
case "$filename" in
  *"-p"*)
    #echo "filename contains '-p'";
    filename=${filename#*"-p"};
    #echo "$filename";
esac

pagevalue=$(echo "$filename" | grep -o -E '[0-9]+') 
i=$pagevalue

####Undoes digit conformity so that math can be performed
#echo "First digit is ${i:0:1}"
while [ ${i:0:1} == "0" ];
do
  i=${i:1:5}
#  echo "Sripping digit conformity. value is now "$i".";
  sleep 0.01;
done
echo "Stripped page number is $i"
####Knocks down by 2s to, at lowest, 0 / 1, so even if it's not got the expected type (odd/even), this will still return the appropriate number.
while [ $i -gt 1 ];
do
  i=$((i-2));
  decreaseLoopRun=$((decreaseLoopRun+1))
#  echo "Decrimenting first page's name to image_"$i".jpg";
  sleep 0.01;
done

i="0$i"
while [ $i == "0" ];
do
  i="0$i"
  sleep 0.01;
done


echo "First page new name is $seriesid-c$chaptnum-p$i.jpg"
echo "Page devalue loop must be run "$decreaseLoopRun" times on all following pages"
mv $originalfilename "tmp/$seriesid-c$chaptnum-p$i.jpg"





#Loop [amount of items in target folder]
pagelist=$(ls)
for file in $pagelist
do

  ####Edit of previous code with modifications to run according to previously gathered data
  filename=$(ls | head -1)
  echo "Working on "$filename

  originalfilename=$filename
  case "$filename" in
    *"-p"*)
      #echo "filename contains '-p'";
      filename=${filename#*"-p"};
      #echo "$filename";
  esac

  pagevalue=$(echo "$filename" | grep -o -E '[0-9]+') 
  i=$pagevalue
  
  ####Undoes digit conformity so that math can be performed
  echo "First digit is ${i:0:1}"
  while [ ${i:0:1} == "0" ];
  do
    i=${i:1:5}
#    echo "Sripping digit conformity. value is now "$i".";
    sleep 0.01;
  done
  
  ####Replicates the effect of the decriment loop, which thanks to the decriment count, can now be replicated with simple math.
  amoutToDecriment=$((decreaseLoopRun * 2))
  i=$((i-amoutToDecriment))

  #Catch under-10s and add a leading 0 to match forced digit conformity of existing system
  if [ $i -lt 10 ];
  then
    i="0$i"
  fi

  echo "Stripped page number is $pagevalue"
  mv $originalfilename "tmp/$seriesid-c$chaptnum-p$i.jpg"
  echo "Next page new name is $seriesid-c$chaptnum-p$i.jpg"

#End Loop
done



#Loop [amount of items in target folder]
cd tmp
pagelist=$(ls)
for file in $pagelist
do
  mv $file ../$file
done

rm -rf ../tmp
