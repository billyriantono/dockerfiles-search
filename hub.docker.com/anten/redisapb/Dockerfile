FROM ansibleplaybookbundle/apb-base

LABEL "com.redhat.apb.spec"=\
"dmVyc2lvbjogMS4wCm5hbWU6IGhhc3RlYmluLWFwYgpkZXNjcmlwdGlvbjogVGhpcyBpcyBhIHNh\
bXBsZSBhcHBsaWNhdGlvbiBnZW5lcmF0ZWQgYnkgYXBiIGluaXQKYmluZGFibGU6IEZhbHNlCmFz\
eW5jOiBvcHRpb25hbAptZXRhZGF0YToKICBkaXNwbGF5TmFtZTogSGFzdGViaW4gKEFQQikKICBk\
ZXBlbmRlbmNpZXM6IFsnZG9ja2VyLmlvL2R5bXVycmF5L2hhc3RlYmluOmxhdGVzdCcsICdkb2Nr\
ZXIuaW8vbW9kdWxhcml0eWNvbnRhaW5lcnMvbWVtY2FjaGVkOmxhdGVzdCddCiAgcHJvdmlkZXJE\
aXNwbGF5TmFtZTogIlJlZCBIYXQsIEluYy4iCnBsYW5zOgogIC0gbmFtZTogZGVmYXVsdAogICAg\
ZGVzY3JpcHRpb246IFRoaXMgZGVmYXVsdCBwbGFuIGRlcGxveXMgaGFzdGViaW4tYXBiCiAgICBm\
cmVlOiBUcnVlCiAgICBtZXRhZGF0YToge30KICAgIHBhcmFtZXRlcnM6CiAgICAgIC0gbmFtZTog\
aGFzdGViaW5fcG9ydAogICAgICAgIHR5cGU6IGludAogICAgICAgIGRlZmF1bHQ6IDc3NzcKICAg\
ICAgICB0aXRsZTogSGFzdGViaW4gUG9ydAogICAgICAtIG5hbWU6IG1heF9sZW5ndGgKICAgICAg\
ICB0eXBlOiBpbnQKICAgICAgICBkZWZhdWx0OiA0MDAwMDAKICAgICAgICB0aXRsZTogTWF4IGxl\
bmd0aCBvZiBoYXN0ZWJpbiBlbnRyeQogICAgICAtIG5hbWU6IGtleV9sZW5ndGgKICAgICAgICB0\
eXBlOiBpbnQKICAgICAgICBkZWZhdWx0OiAxMAogICAgICAgIHRpdGxlOiBMZW5ndGggb2YgaGFz\
dGViaW4ga2V5Cg=="

COPY playbooks /opt/apb/actions
COPY roles /opt/ansible/roles
RUN chmod -R g=u /opt/{ansible,apb}
USER apb
