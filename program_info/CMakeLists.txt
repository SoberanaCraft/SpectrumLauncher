if(UNIX)
    find_package(PkgConfig)
    if(PkgConfig_FOUND)
        pkg_search_module(SCDOC scdoc)
        if(SCDOC_FOUND)
            pkg_get_variable(SCDOC_SCDOC scdoc scdoc)
        endif()
    endif()
endif()

set(Launcher_CommonName "SpectrumLauncher")
set(Launcher_DisplayName "Spectrum Launcher")

set(Launcher_Name "${Launcher_CommonName}" PARENT_SCOPE)
set(Launcher_DisplayName "${Launcher_DisplayName}" PARENT_SCOPE)

set(Launcher_Copyright "BlocoVermelho, Prism Launcher Contributors\\n© 2021-2022 PolyMC Contributors \\n© 2012-2021 MultiMC Contributors")
set(Launcher_Copyright_Mac "BlocoVermelho, Prism Launcher Contributors, © 2021-2022 PolyMC Contributors and © 2012-2021 MultiMC Contributors" PARENT_SCOPE)
set(Launcher_Copyright "${Launcher_Copyright}" PARENT_SCOPE)
set(Launcher_Domain "spectrumlauncher.org" PARENT_SCOPE)
set(Launcher_UserAgent "${Launcher_CommonName}/${Launcher_VERSION_NAME}" PARENT_SCOPE)
set(Launcher_ConfigFile "spectrumlauncher.cfg" PARENT_SCOPE)
set(Launcher_Git "https://github.com/blocovermelho/SpectrumLauncher" PARENT_SCOPE)
set(Launcher_DesktopFileName "org.blocovermelho.SpectrumLauncher.desktop" PARENT_SCOPE)
set(Launcher_SVGFileName "org.blocovermelho.SpectrumLauncher.svg" PARENT_SCOPE)

set(Launcher_Desktop "program_info/org.blocovermelho.SpectrumLauncher.desktop" PARENT_SCOPE)
set(Launcher_mrpack_MIMEInfo "program_info/modrinth-mrpack-mime.xml" PARENT_SCOPE)
set(Launcher_MetaInfo "program_info/org.blocovermelho.SpectrumLauncher.metainfo.xml" PARENT_SCOPE)
set(Launcher_SVG "program_info/org.blocovermelho.SpectrumLauncher.svg" PARENT_SCOPE)
set(Launcher_Branding_ICNS "program_info/spectrumlauncher.icns" PARENT_SCOPE)
set(Launcher_Branding_ICO "program_info/spectrumlauncher.ico")
set(Launcher_Branding_ICO "${Launcher_Branding_ICO}" PARENT_SCOPE)
set(Launcher_Branding_WindowsRC "program_info/spectrumlauncher.rc" PARENT_SCOPE)
set(Launcher_Branding_LogoQRC "program_info/spectrumlauncher.qrc" PARENT_SCOPE)

set(Launcher_Portable_File "program_info/portable.txt" PARENT_SCOPE)

configure_file(org.blocovermelho.SpectrumLauncher.desktop.in org.blocovermelho.SpectrumLauncher.desktop)
configure_file(org.blocovermelho.SpectrumLauncher.metainfo.xml.in org.blocovermelho.SpectrumLauncher.metainfo.xml)
configure_file(spectrumlauncher.rc.in spectrumlauncher.rc @ONLY)
configure_file(spectrumlauncher.manifest.in spectrumlauncher.manifest @ONLY)
configure_file(spectrumlauncher.ico spectrumlauncher.ico COPYONLY)
configure_file(win_install.nsi.in win_install.nsi @ONLY)

if(SCDOC_FOUND)
    set(in_scd "${CMAKE_CURRENT_SOURCE_DIR}/spectrumlauncher.6.scd")
    set(out_man "${CMAKE_CURRENT_BINARY_DIR}/spectrumlauncher.6")
    add_custom_command(
        DEPENDS "${in_scd}"
        OUTPUT "${out_man}"
        COMMAND ${SCDOC_SCDOC} < "${in_scd}" > "${out_man}"
    )
    add_custom_target(man ALL DEPENDS ${out_man})
    set(Launcher_ManPage "program_info/spectrumlauncher.6" PARENT_SCOPE)
endif()
