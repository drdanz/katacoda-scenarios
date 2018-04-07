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

`cmake -H . -B build`{{execute T4}}
`cmake --build build`{{execute T4}}
`build/summer`{{execute T4}}



For now, there's no need to worry too much the details of this code.
Start another two terminals and do the following (make sure the `yarp read` and
`yarp write` programs started earlier are still running):
