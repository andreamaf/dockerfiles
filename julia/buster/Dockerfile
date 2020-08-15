FROM julia:buster AS base

FROM python:slim
COPY --from=base /usr/local/julia /usr/local

#ENV PATH=/usr/local/julia:$PATH
RUN set -eux; \
   apt-get update; \
   apt-get install -y --no-install-recommends \
       ca-certificates \
# ERROR: no download agent available; install curl, wget, or fetch
       curl \
   ; \
   rm -rf /var/lib/apt/lists/*

RUN julia -e 'using Pkg; Pkg.update()' && \
    julia -e 'using Pkg; Pkg.REPLMode.pkgstr("add IJulia           ;precompile"); using IJulia' && \
    julia -e 'using Pkg; Pkg.REPLMode.pkgstr("add Plots            ;precompile"); using Plots' && \
    julia -e 'using Pkg; Pkg.REPLMode.pkgstr("add DataFrames       ;precompile"); using DataFrames' && \
    julia -e 'using Pkg; Pkg.REPLMode.pkgstr("add CSV              ;precompile"); using CSV'

RUN pip3 install jupyter

EXPOSE 8888

CMD jupyter notebook --no-browser --ip=0.0.0.0 --port=8888 --allow-root
