FROM ubuntu:18.04
RUN apt-get update
RUN apt-get install -y curl wget
RUN apt-get install -y build-essential
RUN apt-get install -y libgd-dev
RUN apt-get install -y p7zip-full p7zip-rar
RUN apt-get install -y tree

# Set the working directory to /app
WORKDIR /app


# Copy the current directory contents into the container at /app
COPY . /app

#Make diretory to mount folders
RUN mkdir -p /app/mnt/


#FROM perl:latest
RUN curl -L http://cpanmin.us | perl - App::cpanminus
RUN cpanm FindBin Carp Clone Config::General Cwd Data::Dumper Digest::MD5 File::Basename File::Spec::Functions File::Temp FindBin Font::TTF::Font GD GD::Image Getopt::Long IO::File List::MoreUtils List::Util Math::Round Math::Trig Math::VecStat Math::Bezier Memoize POSIX Params::Validate Pod::Usage Readonly Regexp::Common Statistics::Basic Storable Sys::Hostname Text::Balanced Text::Format Time::HiRes
RUN cpanm Math::Bezier SVG Set::IntSpan

RUN echo 'alias circos="/app/circos-0.69-6/bin/circos"' >> ~/.bashrc
