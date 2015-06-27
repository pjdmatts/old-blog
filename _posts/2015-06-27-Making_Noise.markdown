---
layout: post
title:  "Making Noise"
date:   2015-06-27 15:00:00
categories: noise
---

I have been experimenting with generating different noise processes.

Originally I wrote this code in Matlab but it works in Octave also. It is adapted from the work at [this site][burkardt] with some modifications of my own to fit definitions of colored noise by [Wriley][wriley]

The script *f_alpha_gaussian.m* is used to generate a power law noise process of length *n* and variance *q_d* where the 'color' is defined by *alpha*.

For example to generate a 1000 point  White FM process with variance of 1e-12:

```
x = f_alpha_gaussian(1000, 1e-12, 0);
```

Plotting x results in the following:

![Image description](/images/whiteFm.png)

Compare this with a *Random Walk* process:

```
x = f_alpha_gaussian(1000, 1e-12, -2);
```

Plotting x this time results in the following:

![Image description](/images/rwFm.png)




Colored Noise generating script: *f_alpha_gaussian.m*

    function [ x ] = f_alpha_gaussian( n, q_d, alpha )

    %Adapted with some small modification from the source code
    %listed at:
    %http://people.sc.fsu.edu/~jburkardt/m_src/cnoise/f_alpha_gaussian.m
    %This is based on Kasdins work on simulating power law processes.

    % Purpose:
    %     Generates a discrete colored noise vector of size n with power
    %     spectrum distribution of alpha
    %     White noise is sampled from Gaussian (0,q_d) distribution
    %
    % Usage:
    %        [ x ] = f_alpha_gaussian( n, q_d, alpha )
    %
    %     n - problem size
    %     q_d - variance of the underlying zero-mean Gaussian
    %     alpha - resulting colored noise has 1/f^alpha power spectrum


    %  Set the deviation of the noise.
    %
      q_d = sqrt ( q_d );
    %
    %  Generate the coefficients Hk.
    %

      hfa = zeros ( 2 * n, 1 );
      hfa(1) = 1.0;
      for i = 2 : n
        hfa(i) = hfa(i-1) * ( -0.5 * alpha + ( i - 2 ) ) / ( i - 1 );
      end
      hfa(n+1:2*n) = 0.0;

    %
    %  Fill Wk with white noise.
    %

      wfa = [ q_d * randn( n, 1 ); zeros( n, 1 ); ];
      %wfa = [ q_d * ( 2*rand( n, 1 ) - 1 ); zeros( n, 1 ); ];

    %
    %  Perform the discrete Fourier transforms of Hk and Wk.
    %

      [ fh ] = fft( hfa );
      [ fw ] = fft( wfa );

    %
    %  Multiply the two complex vectors.
    %
        fh = fh( 1:n + 1 );
        fw = fw( 1:n + 1 );

        fw = fh .* fw;

    %
    %  This scaling is introduced only to match the behavior
    %  of the Numerical Recipes code...
    %

        fw(1)       = fw(1) / 2;
        fw(end)     = fw(end) / 2;

    %
    %  Take the inverse Fourier transform of the result.
    %

      fw = [ fw; zeros(n-1,1); ];

      x = ifft( fw );

      x = 2*real( x(1:n) );

    %
    %  Discard the second half of the inverse Fourier transform.
    %

      return
    end

Mixed Noise generation script: *mixedNoise.m*

    function [x] = mixedNoise(steps, alpha_varianceStruct)
    % S is a struct containing the noise processes variance and alpha coeffs
    S = alpha_varianceStruct;
    % N is the length of the desired simulation
    N = length(S.alpha);
    seperateNoiseRuns = zeros(steps, N);
    for i = 1:N
        seperateNoiseRuns(:, i) = f_alpha_gaussian(steps, S.variance(i),...
            S.alpha(i));
    end
    %Add the noise runs together to get the cumulative effect.
    %Assume this is OK?
    x = sum(seperateNoiseRuns, 2);





[noise]:      /code/f_alpha_gaussian.m
[burkardt]:   http://people.sc.fsu.edu/~jburkardt/m_src/cnoise/f_alpha_gaussian.m
[wriley]:     http://tf.nist.gov/general/pdf/2220.pdf
