# dnstop

dnstop is a libpcap application (ala tcpdump) that displays various tables of DNS traffic on your network.

For more information please refer to: [http://dns.measurement-factory.com/tools/dnstop/index.html](http://dns.measurement-factory.com/tools/dnstop/index.html)

# Please read

Initially this is a fork from [verisign/dnstop](https://github.com/verisign/dnstop). I forked this due to the needs to add additional options based on my requirement. However, `verisign/dnstop` was built from `dnstop-20120611` from the original author (link above). So I've updated this fork to include changes from the original author using build from `dnstop-20140915`. I added extra options as well as per my requirement.

# Installing
```
$ ./configure
$ make all
```

Note that you might need to change the `Makefile` generated after running the configure to include `-lpthread` flag under the `LIBS`.

# Extra options
Additional feature is able to save the report in comma separated value for query name report. This is run every 30s or after user defined interval to `/tmp` or user defined location. 

Why? Current build from original author does not allow interactive tty to be piped/redirected to file. I need to run a report based on this, thus the workaround.

Options
```
-z interval Specify the interval for report to be run. Default is 30s
-o dir      Specify directory without trailing slash for report to be saved. Defaul is /tmp
```

Both options can be specified or either one would do. Missing option will use default value. To disable, do not specifiy both.

# Example
```
$ sudo ./dnstop -z 10 -o /tmp/dnstop eth0

Query Name     Count      %   cum%
---------- --------- ------ ------
google.com         1  100.0  100.0
```

Result
```
$ tail 1420619755.txt

google.com,1,100.000000,100.000000
```
