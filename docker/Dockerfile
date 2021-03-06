FROM centos:7

WORKDIR /root

RUN yum update -y && yum install -y epel-release && yum clean all

RUN yum update -y && yum install -y \
    cmake \
    curl-devel \
    expat-devel \
    gcc \
    gcc-c++ \
    gcc-gfortran \
    gettext-devel \
    git \
    make \
    openssl \
    openssl098e \
    openssl-devel \
    patch \
    svn \
    wget \
    which \
    && yum clean all    

ENV PATH /usr/local/sbin:/usr/local/bin:$PATH

ENV LD_LIBRARY_PATH /usr/local/lib:/usr/local/lib64

# Julia
ENV JULIA_VER_MAJ 1.1
ENV JULIA_VER_MIN .0
ENV JULIA_VER $JULIA_VER_MAJ$JULIA_VER_MIN

RUN wget https://julialang-s3.julialang.org/bin/linux/x64/$JULIA_VER_MAJ/julia-$JULIA_VER-linux-x86_64.tar.gz \
    && mkdir /usr/local/julia \
    && tar xf julia-$JULIA_VER-linux-x86_64.tar.gz --directory /usr/local/julia --strip-components=1 \
    && ln -s /usr/local/julia/bin/julia /usr/local/bin/julia \
    && rm -f julia-$JULIA_VER-linux-x86_64.tar.gz

ENV JULIA_PKGDIR /usr/local/julia/share/julia/site

RUN julia -e 'using Pkg; \
    Pkg.add([ \
    PackageSpec(url="https://github.com/OpenMendel/SnpArrays.jl"), \
    PackageSpec(url="https://github.com/OpenMendel/OrdinalMultinomialModels.jl"), \
    PackageSpec(url="https://github.com/OpenMendel/OrdinalGWAS.jl") \
    ]); \
    Pkg.test("OrdinalGWAS");'
