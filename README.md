# 说明

对`spark-2.4.0-bin-hadoop2.7` 中`kubernetes` dockerfile 的修改。

将 `alpine` 换为 `ubuntu:18.10`



# 测试
构建：
```bash
$ ./bin/docker-image-tool.sh -r X.X.X.X/spark -t v2.4.0 build
$ ./bin/docker-image-tool.sh -r X.X.X.X/spark -t v2.4.0 push
```
执行：
```bash
bin/spark-submit \
    --master k8s://https://X.X.X.X:X/r/projects/1a7/kubernetes:6443 \
    --deploy-mode cluster \
    --name spark-pi \
    --conf spark.executor.instances=4 \
    --conf spark.kubernetes.namespace=bigdata \
    --conf spark.kubernetes.container.image=X.X.X.X/spark/spark-py:v2.4.0 \
    --conf spark.kubernetes.pyspark.pythonVersion=3 \
    --conf spark.kubernetes.container.image.pullPolicy=Always \
    --jars local:////opt/spark/examples/jars/spark-examples_2.11-2.4.0.jar  local:////opt/spark/work-dir/pi.py 3
```
