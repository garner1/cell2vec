#/usr/bin/env bash

img=$1 #input image of the single nucleus without the suffix jpg

#this create the raw file fromt the jpg file
python /home/garner1/Work/pipelines/euler/chunkyeuler/scripts/image_stack_to_raw.py ${img}.jpg

#generate the Euler characteristic curve
/home/garner1/Work/pipelines/euler/chunkyeuler/build/CHUNKYEuler -p 1 -f ${img}.jpg_t_u8_1024x1024.from_stack.raw -s '1024 1024 1'

#reformat the Euler characteristic file to include of 256 x values
t=( $(cut -d' ' -f1 ${img}.jpg_t_u8_1024x1024.from_stack.raw.euler | /usr/local/share/anaconda2/bin/datamash transpose) )
c=( $(cut -d' ' -f2 ${img}.jpg_t_u8_1024x1024.from_stack.raw.euler | /usr/local/share/anaconda2/bin/datamash transpose) )
t+=(256)
for i in $(seq 1 ${t[-1]}); do
    for j in $(seq ${t[$i]} $(( ${t[$i+1]}-1 ))); do
    	echo $j ${c[$i]}
    done
done > ${img}.euler.txt

#generate the plot of the curve if needed
python /home/garner1/Work/pipelines/euler/chunkyeuler/scripts/plotEuler.py ${img}.euler.txt

