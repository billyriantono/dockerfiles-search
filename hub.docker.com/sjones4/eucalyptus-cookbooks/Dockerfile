FROM sjones4/chef-dk

ENV EUCALYPTUS_COOKBOOK=/root/eucalyptus-cookbook \
    EUCALYPTUS_COOKBOOK_TGZ=eucalyptus-cookbooks.tgz

WORKDIR /eucalyptus-cookbook

# Note that we are installing chefdk 2.5.3 with broken chefinclude
# support. Once we stop ignoring faststart files we can update to
# use the latest https://downloads.chef.io/chefdk#el
RUN git clone --depth 1 -- https://github.com/corymbia/eucalyptus-cookbook.git "${EUCALYPTUS_COOKBOOK}" \
 && sed --in-place '2isolver :ruby' "${EUCALYPTUS_COOKBOOK}/Berksfile" \
 && berks package -b "${EUCALYPTUS_COOKBOOK}/Berksfile" "${EUCALYPTUS_COOKBOOK_TGZ}" \
 && cp -fv "${EUCALYPTUS_COOKBOOK}/faststart/cloud-in-a-box.sh" "cloud-in-a-box.sh" \
 && rm -rf "${EUCALYPTUS_COOKBOOK}" /root/.berkshelf

