# test-pqpki version 1.0.0

Thank you for your interest in the Post-Quantum PKI Test server!  You can find
out more at http://test-pqpki.com/.  If you have further questions, contact
test-pqpki@isara.com.  This README is a quick overview of how to build example
client apps and libraries to interact with the server.

Get the test-pqpki patches (if you're reading this you may have already done
this):

<pre>
git clone https://github.com/isaracorp/test-pqpki.git
</pre>

Get the test-pqpki openssl and libest repos and apply the test-pqpki patches:

<pre>
git clone https://github.com/isaracorp/openssl.git -b test-pqpki-v1.0.0
cd openssl
git apply ../test-pqpki/v1.0.0/test-pqpki-openssl.patch
cd ..
git clone https://github.com/cisco/libest.git -b rel-2.1.0
cd libest
git apply ../test-pqpki/v1.0.0/test-pqpki-libest.patch
cd ..
</pre>

Build openssl (your method may vary, e.g. libest requires 64-bit openssl, so
on MacOS you'll need to use './Configure darwin64-x86_64-cc' rather than
'./config'):

<pre>
cd openssl
./config --prefix=/usr/local/pqpki-openssl1.0.2o \
    --openssldir=/usr/local/pqpki-openssl1.0.2o shared
make
sudo make install
cd ..
</pre>

Build libest:

<pre>
cd libest
./configure --with-ssl-dir=/usr/local/pqpki-openssl1.0.2o
make
cd ..
</pre>

Run our test script to exercise the test-pqpki.com server if you want:

<pre>
cd libest
PATH=/usr/local/pqpki-openssl1.0.2o/bin:$PATH ./mpkac_test.sh
cd ..
</pre>
