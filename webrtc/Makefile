#!/bin/sh
PREBUILT="D:/tools/android-ndk-r10/toolchains/arm-linux-androideabi-4.6/prebuilt/windows"
PLATFORM="D:/tools/android-ndk-r10/platforms/android-8/arch-arm"

CROSS = $(PREBUILT)/bin
CC = $(CROSS)/arm-linux-androideabi-gcc
AR = $(CROSS)/arm-linux-androideabi-ar
LDFLAGS ="-Wl,-T,$(PREBUILT)/arm-linux-androideabi/lib/ldscripts/armelf_linux_eabi.x -Wl,-rpath-link=$(PLATFORM)/usr/lib -L$(PLATFORM)/usr/lib -nostdlib $(PREBUILT)/lib/gcc/arm-linux-androideabi/4.6/crtbegin.o $(PREBUILT)/lib/gcc/arm-linux-androideabi/4.6/crtend.o -lc -lm -ldl" 
INC += -I./ortp
INC += -I$(PLATFORM)/usr/include

LOCAL_SRC_FILES := \
    aec/echo_cancellation.c \
    aec/aec_resampler.c \
    aec/aec_core.c \
    aec/aec_rdft.c \
    aecm/echo_control_mobile.c \
    aecm/aecm_core.c \
    aecm/aecm_core_neon.c \
    agc/analog_agc.c \
    agc/digital_agc.c \
    ns/noise_suppression_x.c \
    ns/nsx_core.c \
    ns/nsx_core_neon.c \
    utility/fft4g.c \
    utility/ring_buffer.c \
    utility/delay_estimator.c \
    utility/delay_estimator_wrapper.c \
    common_audio/signal_processing/auto_corr_to_refl_coef.c \
    common_audio/signal_processing/auto_correlation.c \
    common_audio/signal_processing/complex_fft.c \
    common_audio/signal_processing/copy_set_operations.c \
    common_audio/signal_processing/cross_correlation.c \
    common_audio/signal_processing/division_operations.c \
    common_audio/signal_processing/dot_product_with_scale.c \
    common_audio/signal_processing/downsample_fast.c \
    common_audio/signal_processing/energy.c \
    common_audio/signal_processing/filter_ar.c \
    common_audio/signal_processing/filter_ma_fast_q12.c \
    common_audio/signal_processing/get_hanning_window.c \
    common_audio/signal_processing/get_scaling_square.c \
    common_audio/signal_processing/ilbc_specific_functions.c \
    common_audio/signal_processing/levinson_durbin.c \
    common_audio/signal_processing/lpc_to_refl_coef.c \
    common_audio/signal_processing/min_max_operations.c \
    common_audio/signal_processing/randomization_functions.c \
    common_audio/signal_processing/real_fft.c \
    common_audio/signal_processing/refl_coef_to_lpc.c \
    common_audio/signal_processing/resample.c \
    common_audio/signal_processing/resample_48khz.c \
    common_audio/signal_processing/resample_by_2.c \
    common_audio/signal_processing/resample_by_2_internal.c \
    common_audio/signal_processing/resample_fractional.c \
    common_audio/signal_processing/spl_init.c \
    common_audio/signal_processing/spl_sqrt.c \
    common_audio/signal_processing/spl_version.c \
    common_audio/signal_processing/splitting_filter.c \
    common_audio/signal_processing/sqrt_of_one_minus_x_squared.c \
    common_audio/signal_processing/vector_scaling_operations.c \
    common_audio/signal_processing/filter_ar_fast_q12.c \
    common_audio/signal_processing/complex_bit_reverse_arm.s \
    common_audio/signal_processing/spl_sqrt_floor_arm.s \
    common_audio/signal_processing/cross_correlation_neon.s \
    common_audio/signal_processing/downsample_fast_neon.s \
    common_audio/signal_processing/min_max_operations_neon.s \
    common_audio/signal_processing/vector_scaling_operations_neon.s
   
LOCAL_CFLAGS := \
    $(MY_WEBRTC_COMMON_DEFS) \
    -mfpu=neon \
    -mfloat-abi=softfp \
    -flax-vector-conversions \
    -DWEBRTC_ANDROID
    
INC += \
		-I./aec/include \
		-I./aecm/include \
		-I./agc/include \
		-I./ns/include \
    -I./include \
    -I./utility \
    -I./common_audio/signal_processing/include \
    -I./interface
	
webrtc.o : $(LOCAL_SRC_FILES)
	$(CC) -c -O3 $(LOCAL_SRC_FILES) $(INC) $(LDFLAGS) $(LOCAL_CFLAGS)
	
	$(AR) rcs libwebrtc.a *.o
clean:
	rm *.o