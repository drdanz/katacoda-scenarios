In this step you will install YARP

Add robotology repository:
`echo "deb http://www.icub.org/ubuntu xenial contrib/science" > /etc/apt/sources.list.d/icub.list`{{execute}}

Add robotology GPG key:
`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 57A5ACB6110576A6`{{execute}}

Update apt repository list:
`apt-get update`{{execute}}

Install yarp:
`apt-get install -y yarp`{{execute}}

Check yarp installed version:
`yarp version`{{execute}}


<pre class="file" data-filename="summer.cpp" data-target="replace">


#include <yarp/os/all.h>
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
          


<pre class="file" data-target="clipboard">Test</pre>
          


<pre class="file" data-target="regex???">Test</pre>
          

