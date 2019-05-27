# Support for non-standard ports {#concept_ild_n1l_l2b .concept}

In addition to ports 80/8080 \(HTTP\) and 443/8443 \(HTTPS\), Anti-Bot Service also provides protection for specific non-standard ports.

Each Anti-Bot instance supports up to 50 ports, including standard ports 80, 8080, 443, and 8443.

**Note:** Anti-Bot Service only provides protection for supported ports. Requests from unsupported ports are not accepted or forwarded. For example, when an Anti-Bot instance receives a request from port 4444, the request is discarded.

## Supported HTTP ports {#section_x4f_41l_l2b .section}

Anti-Bot Service supports the following HTTP ports:

80, 81, 82, 83, 84, 88, 89, 800, 808, 1000, 1090, 3333, 3501, 3601, 5000, 5222, 6001, 6666, 7000, 7001, 7002, 7003, 7004, 7005, 7006, 7009, 7010, 7011, 7012, 7013, 7014, 7015, 7016, 7018, 7019, 7020, 7021, 7022, 7023, 7024, 7025, 7026, 7070, 7081, 7082, 7083, 7088, 7097, 7777, 7800, 8000, 8001, 8002, 8003, 8008, 8009, 8020, 8021, 8022, 8025, 8026, 8077, 8078, 8080, 8081, 8082, 8083, 8084, 8085, 8086, 8087, 8088, 8089, 8090, 8091, 8106, 8181, 8334, 8336, 8800, 8686, 8888, 8889, 8999, 9000, 9001, 9002, 9003, 9080, 9200, 9999, 10000, 10001, 10080, 12601, 86, 9021, 9023, 9027, 9037, 9081, 9082, 9201, 9205, 9207, 9208, 9209, 9210, 9211, 9212, 9213, 48800, 87, 97, 7510, 9180, 9898, 9908, 9916, 9918, 9919, 9928, 9929, 9939, 28080, 33702

## Supported HTTPS ports {#section_z4f_41l_l2b .section}

Anti-Bot Service supports the following HTTPS ports:

443, 4443, 5443, 6443, 7443, 8443, 9443, 8553, 8663, 9553, 9663, 18980

