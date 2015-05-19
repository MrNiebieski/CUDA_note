#CUDA profiling tools:#

quick start guide:

I have problem with visual profiling:

    java: cairo-misc.c:380 _cairo_operator_bounded_by_source: Assertion `NOT_REACHED` failed.

so, I am using `nvprof` to generate report first, and then view in the visual profiler.


    nvprof --output-profile <profileName> ./<excutableToBeProfiled> <argument>

then start `nvvp` (GUI)

`import` from `nvprof` to view report.


###concentrated profile###

add:

    #include <cuda_profiler_api.h>

then add:


    cudaProfilerStart();
    // code
    cudaProfilerStop();


###register count###

in `Makefile` add:

    NVCCFLAGS = -O3 -g -arch=sm_35 -Xptxas="-v"

`-Xptxas="-v"` will count register use when compile.

use with `grep`

    make 2>&1|grep -e register -e Function