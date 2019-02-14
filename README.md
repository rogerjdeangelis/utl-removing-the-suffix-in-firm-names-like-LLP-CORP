# utl-removing-the-suffix-in-firm-names-like-LLP-CORP
Removing the suffix in firm names like LLP CORP
    Removing the suffix in firm names like LLP CORP

    github
    https://tinyurl.com/y377qt8h
    https://github.com/rogerjdeangelis/utl-removing-the-suffix-in-firm-names-like-LLP-CORP

    SAS Forum
    https://tinyurl.com/yycvv7no
    https://communities.sas.com/t5/SAS-Programming/Removing-abbreviations-in-firms-names-more-questions/m-p/535589

    INPUT
    =====

    * The sufixes to remove;

    array sfxs $16 a1-a24 ('AG' ,'BV' ,'CORPORATION' ,'GMBH' ,'INC' ,'LIMITED' ,'LLC'
    ,'LP' ,'LTD' ,'PJSC' ,'PLC' ,'PTE' ,'PTY' ,'SA' ,'SA/NV' ,'SL'
    ,'SPA' ,'SRL' ,'COMPANY' ,'VLP' ,'CO' ,'NV' ,'HOLDINGS' ,'HOLDING');

    data firms;
      input firmname & $100.;
    cards4;
    AXXAM SPA
    AXXESS COMPOUNDING LP
    AXXIMA PHARMACEUTICALS AG
    BEAR STEARNS HEALTH INNOVENTURES LP
    BEAUBRIDGE LLP
    CANNAVEST CORP
    CARESTIA SA
    COMIFAR SPA
    DUTALYS GMBH
    ESSEX CHEMIE AG
    IMAGING3 INC
    ;;;;
    run;quit;

     WORK.FIRMS total obs=11

      FIRMNAME

      AXXAM SPA
      AXXESS COMPOUNDING LP
      AXXIMA PHARMACEUTICALS AG
      BEAR STEARNS HEALTH INNOVENTURES LP
      BEAUBRIDGE LLP
      CANNAVEST CORP
      CARESTIA SA
      COMIFAR SPA
      DUTALYS GMBH
      ESSEX CHEMIE AG
      IMAGING3 INC


    EXAMPLE OUTPUT
    --------------

    WORK,WANT total obs=11

      FIRMNAME

      AXXAM
      AXXESS COMPOUNDING
      AXXIMA PHARMACEUTICALS
      BEAR STEARNS HEALTH INNOVENTURES

      BEAUBRIDGE LLP                   **** LLP Not in list
      CANNAVEST CORP                   **** CORP Not in list

      CARESTIA
      COMIFAR
      DUTALYS
      ESSEX CHEMIE
      IMAGING3

    SOLUTION
    =========

    data want;

      array sfxs $16 a1-a24 ('AG' ,'BV' ,'CORPORATION' ,'GMBH' ,'INC' ,'LIMITED' ,'LLC'
         ,'LP' ,'LTD' ,'PJSC' ,'PLC' ,'PTE' ,'PTY' ,'SA' ,'SA/NV' ,'SL'
         ,'SPA' ,'SRL' ,'COMPANY' ,'VLP' ,'CO' ,'NV' ,'HOLDINGS' ,'HOLDING');

      set firms;

      call scan(firmname, -1, position, length, ' ');

      if substr(firmname,position,length) in sfxs then firmname=substr(firmname,1,position-1);
      keep firmname;

    run;quit;



