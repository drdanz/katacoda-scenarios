Create the following files:

<pre class="file" data-filename="summer.cpp" data-target="replace">#include &lt;yarp/os/Network.h&gt;
#include &lt;yarp/os/BufferedPort.h&gt;
#include &lt;yarp/os/Bottle.h&gt;
#include &lt;iostream&gt;

using yarp::os::Network;
using yarp::os::BufferedPort;
using yarp::os::Bottle;

int main(int argc, char* argv[])
{
    Network yarp;
    BufferedPort&lt;Bottle&gt; port;
    port.open("/summer");
    while (true) {
        std::cout << "waiting for input" << std::endl;
        Bottle* input = port.read();
        if (input != NULL) {
            std::cout << "got " << input->toString().c_str() << std::endl;
            double total = 0;
            for (int i = 0; i < input->size(); i++) {
                total += input->get(i).asDouble();
            }
            Bottle& output = port.prepare();
            output.clear();
            output.addString("total");
            output.addDouble(total);
            std::cout << "writing " << output.toString().c_str() << std::endl;
            port.write();
        }
    }
    return 0;
}
</pre>

<pre class="file" data-filename="CMakeLists.txt" data-target="replace">cmake_minimum_required(VERSION 3.0)

project(summer)

find_package(YARP REQUIRED)

add_executable(summer summer.cpp)
target_link_libraries(summer YARP::YARP_OS
                             YARP::YARP_init)
</pre>

For now, there's no need to worry too much the details of this code.
Start another two terminals and do the following (make sure the `yarp read` and
`yarp write` programs started earlier are still running):


On terminal 4 run:

* `mkdir build`{{execute T4}}
* `cd build`{{execute T4}}
* `cmake ..`{{execute T4}}
* `make`{{execute T4}}
* `./summer`{{execute T4}}

On terminal #5 run:

* `yarp connect /write /summer`{{execute T5}}
* `yarp connect /summer /read`{{execute T5}}


The network is now as follows:
![Adding the "summer" program](https://raw.githubusercontent.com/drdanz/katacoda-scenarios/master/hello-world/dot_inline_dotgraph_6.png)


If you type a list of numbers the "yarp write" terminal, they will show up on
the `yarp read` terminal as before.
But they will also be sent to the "summer" process, which will send an extra
message to the `yarp read` terminal. For example, if on terminal 3
(`yarp write`) you type: `10 -5 17.15 6`{{execute T3}}, on terminal 2
(`yarp read`), you will see:

```
10 -5 17.15 6
total 28.15
```

(the order of these messages is random).
