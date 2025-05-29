# Experiments-with-Sin-Generatore

#include <stdio.h>
#include <math.h>

int main(void)
{
    FILE *out;
    float sample = 0.0;

    out = fopen("Sound2.bin", "wb");

    float sampleRate = 48000.0;
    float f_start = 1.0;
    float f_end = 48000.0;
    float duration = 60.0;
    float numberOfSamples = sampleRate * duration;
    float k;
    float t;
    float freq;
    float phi = 0.0;

    k = log(f_end / f_start) / duration;

    for(int i = 0; i < numberOfSamples; i++)
    {
        t = (float)i / sampleRate;
        freq = f_start * exp(k * t);
        phi = phi + (2 * M_PI * freq / sampleRate);

        if(phi > (2 * M_PI))
        {
            phi = phi - (2 * M_PI);
        }
        sample = sin(phi);
        fwrite(&sample, sizeof(float), 1, out);
    }
    
    printf("Done!!\n");

    fclose(out);
    return 0;
}
