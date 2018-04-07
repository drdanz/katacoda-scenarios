<pre class="file" data-filename="summer/summer.cpp" data-target="replace">#include <yarp/os/all.h>
#include <iostream>
using namespace std;
using namespace yarp::os;
int main(int argc, char *argv[]) {
    Network yarp;
    BufferedPort<Bottle> port;
    port.open("/summer");
    while (true) {
        cout << "waiting for input" << endl;
        Bottle *input = port.read();
        if (input!=NULL) {
            cout << "got " << input->toString().c_str() << endl;
            double total = 0;
            for (int i=0; i<input->size(); i++) {
                total += input->get(i).asDouble();
            }
            Bottle& output = port.prepare();
            output.clear();
            output.addString("total");
            output.addDouble(total);
            cout << "writing " << output.toString().c_str() << endl;
            port.write();
        }
    }
    return 0;
}
</pre>

<pre class="file" data-filename="summer/CMakeLists.txt" data-target="replace">cmake_minimum_required(VERSION 3.0)

project(summer)

find_package(YARP REQUIRED)

add_executable(summer summer.cpp)
target_link_libraries(summer YARP::YARP_OS
                             YARP::YARP_init)
</pre>

`cmake -H summer -B summer/build`{{execute}}
`cmake --build summer/build`{{execute}}
`summer/build/summer`{{execute}}



For now, there's no need to worry too much the details of this code.
Start another two terminals and do the following (make sure the `yarp read` and
`yarp write` programs started earlier are still running):
