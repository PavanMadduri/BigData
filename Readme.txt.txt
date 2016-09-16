First Run mapper of phase1 and reduce files then the output is fed to mapper of phase2 and reduce

hadoop jar /usr/hdp/2.3.0.0-2557/hadoop-mapreduce/hadoop-streaming-2.7.1.2.3.0.0-2557.jar -D mapred.map.tasks=2 -D mapred.reduce.tasks=1 -files "<phase_1 map_location>","<phase_1 reduce_location>" -mapper "<Map_1 filename>" -reducer "<reduce_1 file name>" -input <input file> -output <output file>

hadoop fs -get /market/output/part-00000 <destination>


hadoop jar /usr/hdp/2.3.0.0-2557/hadoop-mapreduce/hadoop-streaming-2.7.1.2.3.0.0-2557.jar -D mapred.map.tasks=2 -D mapred.reduce.tasks=1 -files "<pahse_2 map>","<phase_2 reduce>",-cacheFile <output of fist phase>#<tag_name> -mapper "<phase_2 map file>" -reducer "<phase_2 reduce file>" -input <input file> -output <output_file>


In our case:

hadoop jar $HADOOP_HOME/contrib/streaming/hadoop-*-streaming.jar -D mapred.map.tasks=2 -D mapred.reduce.tasks=1 -files "/home/gpadmin/SON/mapper_phase1.py","/home/gpadmin/SON/reducer_phase1.py" -mapper "mapper_phase1.py" -reducer "reducer_phase1.py" -input /input/market.txt -output /input/market/output5/


hadoop fs -get /input/market/output3/part-00000 .


hadoop jar $HADOOP_HOME/contrib/streaming/hadoop-*-streaming.jar  -D mapred.map.tasks=2 -D mapred.reduce.tasks=1 -files "./part-00000","/home/gpadmin/SON/mapper_phase2.py","/home/gpadmin/SON/reducer_phase2.py" -mapper "mapper_phase2.py" -reducer "reducer_phase2.py" -input /input/market.txt -output /input/market/output6/