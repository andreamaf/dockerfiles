# first stage
FROM julia:bullseye AS basejulia

RUN julia -e 'using Pkg; Pkg.update()' && \
    julia -e 'using Pkg; Pkg.REPLMode.pkgstr("add IJulia           ;precompile"); using IJulia' && \
    julia -e 'using Pkg; Pkg.REPLMode.pkgstr("add Plots            ;precompile"); using Plots' && \
    julia -e 'using Pkg; Pkg.REPLMode.pkgstr("add DataFrames       ;precompile"); using DataFrames' && \
    julia -e 'using Pkg; Pkg.REPLMode.pkgstr("add CSV              ;precompile"); using CSV'

# second stage
FROM python:slim

# copy julia bin and dependencies from the 1st stage image
COPY --from=basejulia /usr/local/julia /usr/local
COPY --from=basejulia /root/.julia /root

COPY requirements.txt .
# install dependencies to the local user directory (eg. /root/.local)
RUN pip install --user -r requirements.txt

EXPOSE 8888

CMD jupyter notebook --no-browser --ip=0.0.0.0 --port=8888 --allow-root
