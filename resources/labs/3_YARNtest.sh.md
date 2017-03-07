```
#!/bin/sh
# Confirm the path values given below correspond to your installation

MR=/opt/cloudera/parcels/CDH/lib/hadoop-mapreduce
CDH_BIN=/opt/cloudera/parcels/CDH/bin

# 10 GB specified: 10737418240 bytes
BYTES_TO_GENERATE=10737418240

# Teragen generates 100B files, so lets devide input number
TERAGEN_SIZE=`echo "($BYTES_TO_GENERATE*0.01)/1" | bc`

# Path for intermediate data - I use /tmp taht is public in my config
TMP_DATA_PATH=/tmp

# Mark start of the loop
echo Testing loop started on `date`

# Mapper containers 24 is max. containers on my cluster so 23 is max mappers if I want to keep one slot for application manager
for i in 8 23  
do
   # Reducer containers
   for j in 1 23
   do                 
      # Container memory
      for k in 512 1024 
      do                         
         # Set mapper JVM heap 
         MAP_MB=`echo "($k*0.8)/1" | bc` 

         # Set reducer JVM heap 
         RED_MB=`echo "($k*0.8)/1" | bc`
		 
		 echo "Running TERAGEN: "
		 echo "   - Data generated [bytes]: "$BYTES_TO_GENERATE
		 echo "   - Records generated [records]: "$TERAGEN_SIZE
		 echo "   - YARN container size [MB]: "$k
		 echo "   - Mappers used [num. mappers]: "$i
		 echo "   - Mapper max. heap size [MB]: "$MAP_MB

        time ${CDH_BIN}/yarn jar ${MR}/hadoop-mapreduce-examples.jar teragen \
                     -Dmapreduce.job.maps=$i \
                     -Dmapreduce.map.memory.mb=$k \
                     -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
                     $TERAGEN_SIZE ${TMP_DATA_PATH}/tg-${TERAGEN_SIZE}-${i}-${j}-${k} 1> tera_${TERAGEN_SIZE}_${i}_${j}_${k}.out 2> tera_${TERAGEN_SIZE}_${i}_${j}_${k}.err                       
		
		 echo "Running TERASORT: "
		 echo "   - Data sorted [bytes]: "$BYTES_TO_GENERATE
		 echo "   - Records sorted [records]: "$TERAGEN_SIZE
		 echo "   - YARN container size [MB]: "$k
		 echo "   - Mappers used [num. mappers]: not configurable - depends on block count"
		 echo "   - Mapper max. heap size [MB]: "$MAP_MB
		 echo "   - Reducers used [num. mappers]: "$j
		 echo "   - Mapper max. heap size [MB]: "$MAP_MB
        time ${CDH_BIN}/yarn jar ${MR}/hadoop-mapreduce-examples.jar terasort \
                     -Dmapreduce.job.reduces=$j \
                     -Dmapreduce.map.memory.mb=$k \
                     -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
                     -Dmapreduce.reduce.memory.mb=$k \
                     -Dmapreduce.reduce.java.opts.max.heap=$RED_MB \
	             ${TMP_DATA_PATH}/tg-${TERAGEN_SIZE}-${i}-${j}-${k}  \
                     ${TMP_DATA_PATH}/ts-${TERAGEN_SIZE}-${i}-${j}-${k} 1>> tera_${TERAGEN_SIZE}_${i}_${j}_${k}.out 2>> tera_${TERAGEN_SIZE}_${i}_${j}_${k}.err                         

        $CDH_BIN/hadoop fs -rm -r -skipTrash ${TMP_DATA_PATH}/tg-${TERAGEN_SIZE}-${i}-${j}-${k}                         
        $CDH_BIN/hadoop fs -rm -r -skipTrash ${TMP_DATA_PATH}/ts-${TERAGEN_SIZE}-${i}-${j}-${k}                 
      done
   done
done

echo Testing loop ended on `date`
```