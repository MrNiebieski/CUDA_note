#constant memory:#

in `.cu` file (the declarition of `constant memory` is outside any function):

    __constant__ float dc_Kernel[KERNEL_LENGTH];

    extern "C" void setKernel(float *h_Kernel) {
        cudaMemcpyToSymbol(dc_Kernerl, h_Kernel, KERNEL_LENGTH * sizeof(float));
    }


in `.cpp` file:

    float *h_Kernel;
    h_Kernel = (float *) malloc(KERNEL_LENGTH * sizeof(float));


    //initiate h_Kernel[] on CPU;
    setKernel(h_Kernel);


compare to `global memory` copy (in `.cpp` file):

    cudaMemcpy(d_Input,  h_Input,  imageW*imageH*sizeof(float), cudaMemcpyHostToDevice));
    cudaMemcpy(h_Output, d_Output, imageW*imageH*sizeof(float), cudaMemcpyDeviceToHost));


There is no need to free constant memory.
