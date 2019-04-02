# Self-driving training models {#concept_cbl_d12_2hb .concept}

Assume that a company features self-driving to collect large amounts of data by using devices, such as car cameras, radars, and infrared devices. Additionally, the company decides to invest in self-driving models by using machine learning or deep learning. The size of the collected data is small and the number of generated files is large. Additionally, these files require high-concurrency access.

Generally, a GPU cluster that includes a scale of 100 containers is applied with computational frameworks, such as TensorFlow, caffe2, and mxnet to address these types of issues.

CPFS enables you to store 10 million small files whose size is less than 200 KB. CPFS can provide an IOPS of 300,000 and a maximum throughput of 5 Gbit/s. In typical AI-powered training scenarios, the latency of open, read, and close operations on small files is reduced by eight times, and the training speed is increased by approximately three times.

