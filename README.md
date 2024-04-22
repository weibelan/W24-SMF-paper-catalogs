# W24-SMF-paper-catalogs
Photometric catalogs with bagpipes output used to compute SMFs in https://ui.adsabs.harvard.edu/abs/2024arXiv240308872W/abstract. 
See there for details on the catalog production. A description of the columns is provided below. 
Here, we only share a subset of each catalog, selected to contain objects at z > 3. The selection criteria are outlined in Section 
2.3 of the paper. In terms of the catalog columns, the selection corresponds to

1) z_phot_eazy > 3
2) P(z_phot_eazy > 2.5) > 0.8
3) sn_lw_det_img > 10
4) flag_f115w = flag_f150w = flag_f200w = flag_f277w = flag_f356w = flag_f444w = 0
5) sn_flag = stellar_flag = hugekron_flag = nofit_flag = junk_flag = 0

Therefore, use_phot=1 and the '*_flag' columns are =0 for all the objects in the catalogs by design of the selection.

Below is a description of the columns, where fil stands for the respective filter key in lowercase letters (e.g., f444w).

id                          n/a                 identification number from the SExtractor run
ra                          deg                 right ascension (J2000, SExtractor)
dec                         deg                 declination (J2000, SExtractor)
x_image                     pixel               centroid x-position of the object (SExtractor)
y_image                     pixel               centroid y-position of the object (SExtractor)
a_image                     pixel               isophotal image major axis (SExtractor)
b_image                     pixel               isophotal image minor axis (SExtractor)
theta_image                 deg                 isophotal image position angle (SExtractor)
kron_radius                 n/a                 Kron radius in units of A or B (SExtractor)
sn_lw_det_img	    	        n/a			            S/N in the LW detection image (inverse variance weighted F277W+F356W+F444W stack)
aper_corr                   n/a                 aperture correction factor derived from a (PSF-matched version of) the detection image and applied to all bands
enclosed_flux_fraction      n/a			            fraction of energy encircled by the Kron-ellipse on the F444W PSF. To get the total (multiplicative)
                                                correction applied to the aperture fluxes, use aper_corr / enclosed_flux_fraction

class_star_<fil>	          n/a	                CLASS_STAR parameter (SExtractor), use with caution
faper_<fil>		              nJy			            flux in <fil> measured in a circular aperture of radius 0.16"
eaper_<fil>		              nJy		              error in the aperture flux
f_<fil>		                  nJy		              aperture-corrected, psf-matched flux in <fil>
e_<fil>			                nJy			            error in the aperture-corrected, psf-matched flux in <fil>, with a 5% error floor
sn_<fil>		                n/a			            signal-to-noise ratio in <fil> before applying the 5% error floor
r50_<fil>		                pixel		            radius containing 50% of the flux in <fil> (SExtractor)

sn_flag			                binary		          1, if the corresponding source has S/N < 3 in ALL the NIRCam wide filters F115W, F150W, F200W, F277W, F356W and F444W

flag_<fil>		              binary		          1, if the corresponding source is flagged in <fil>. In this case f_<fil> = e_<fil> = -99		
c_<fil>			                n/a			            compactness parameter f(D=0.4") / f(D=0.2") for LRD selection

z_phot_eazy                 n/a                 best-fit photometric redshift (peak of the PDF, eazy)
z_phot_160_eazy             n/a                 16th percentile of the redshift PDF (eazy)
z_phot_840_eazy             n/a                 84th percentile of the redshift PDF (eazy)
z_phot_chi2_eazy            n/a                 chi^2 of the best-fit photometric redshift (eazy)
f_restU_eazy                nJy                 restframe U-flux (eazy)
e_restU_eazy                nJy                 error in the restframe U-flux (eazy)
f_restB_eazy                nJy                 restframe B-flux (eazy)
e_restB_eazy                nJy                 error in the restframe B-flux (eazy)
f_restV_eazy                nJy                 restframe V-flux (eazy)
e_restV_eazy                nJy                 error in the restframe V-flux (eazy)
f_restJ_eazy                nJy                 restframe J-flux (eazy)
e_restJ_eazy                nJy                 error in the restframe J-flux (eazy)
Lv_eazy			                L_sun	              V-band luminosity (rest-frame, eazy)
Av_eazy			                mag		              extinction in V-band (rest-frame, eazy)
m_star_eazy		              M_sun		            stellar mass (eazy)
m_star_160_eazy	            M_sun		            16th percentile of the stellar mass (eazy)
m_star_840_eazy		          M_sun		            84th percentile of the stellar mass (eazy)
sfr_eazy	                  M_sun/yr		        star formation rate (eazy)
sfr_160_eazy	              M_sun/yr		        16th percentile of the star formation rate (eazy)
sfr_840_eazy	              M_sun/yr		        84th percentile of the star formation rate (eazy)
chi2_eazy_phoenix_stars	    n/a			            Chi^2 of the eazy fit using phoenix star templates
stellar_flag		            binary		          if 1, the source is likely a star, diffraction spike or contaminated by stellar light
hugekron_flag		            binary		          if 1, R50(F444W) > 50 pix or r_kron,red > 150 pix
nofit_flag		              binary		          if 1, eazy did not return a reasonable fit for this source (best-fit redshift -1 or 19.9)
junk_flag		                binary		          if 1, R_50(F444W) < 1.2 and mag(F444W) < 28.5
use_phot		                binary		          if 1, the source is likely a galaxy with reliable photometry (see above)

Additional columns are direct output from bagpipes which we run with the settings described in Section 2.4 of the paper. 

See the bagpipes documentation for more information: https://bagpipes.readthedocs.io/en/latest/
