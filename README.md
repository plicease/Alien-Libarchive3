# Alien::Libarchive3 [![Build Status](https://secure.travis-ci.org/plicease/Alien-Libarchive3.png)](http://travis-ci.org/plicease/Alien-Libarchive3)

Find or install libarchive version 3.x or better

# SYNOPSIS

In your Build.PL:

    use Module::Build;
    use Alien::Libarchive3;
    my $builder = Module::Build->new(
      ...
      configure_requires => {
        'Alien::Libarchive3' => '0',
        ...
      },
      extra_compiler_flags => Alien::Libarchive3->cflags,
      extra_linker_flags   => Alien::Libarchive3->libs,
      ...
    );
    
    $build->create_build_script;

In your Makefile.PL:

    use ExtUtils::MakeMaker;
    use Config;
    use Alien::Libarchive3;
    
    WriteMakefile(
      ...
      CONFIGURE_REQUIRES => {
        'Alien::Libarchive3' => '0',
      },
      CCFLAGS => Alien::Libarchive3->cflags . " $Config{ccflags}",
      LIBS    => [ Alien::Libarchive3->libs ],
      ...
    );

In your script or module:

    use Alien::Libarchive3;
    use Env qw( @PATH );
    
    unshift @PATH, Alien::Libarchive3->bin_dir;

In your [FFI::Platypus](https://metacpan.org/pod/FFI::Platypus) script or module:

    use FFI::Platypus;
    use Alien::Libarchive3;
    
    my $ffi = FFI::Platypus->new(
      lib => [ Alien::Libarchive3->dynamic_libs ],
    );

# DESCRIPTION

This distribution provides libarchive so that it can be used by other 
Perl distributions that are on CPAN.  It does this by first trying to 
detect an existing install of libarchive on your system.  If found it 
will use that.  If it cannot be found, the source code will be downloaded
from the internet and it will be installed in a private share location
for the use of other modules.

The intention is for this to eventually replace [Alien::Libarchive](https://metacpan.org/pod/Alien::Libarchive)

# SEE ALSO

[Alien](https://metacpan.org/pod/Alien), [Alien::Base](https://metacpan.org/pod/Alien::Base), [Alien::Build::Manual::AlienUser](https://metacpan.org/pod/Alien::Build::Manual::AlienUser)

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2017 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
